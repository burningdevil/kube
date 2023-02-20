# Falco

## Getting started

Falco can detect and alert on any behavior that involves making Linux system calls. Falco alerts are triggered based on specific system calls, arguments, and properties of the calling process. Falco operates at the user space and kernel space
![Architecture](https://falco.org/docs/images/falco_architecture.png)

## Falco Rules

A falco rules file is a YAML file containing mainly three types of elements.

| Element | Description                                                                                                                                                        |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Rules   | Conditions under which an alert should be generated. A rule is accompanied by a descriptive output string that is sent with the alert.                             |
| Macros  | Rule condition snippets that can be re-used inside rules and even other macros. Macros provide a way to name common patterns and factor out redundancies in rules. |
| Lists   | Collections of items that can be included in rules, macros, or other lists. Unlike rules and macros, lists cannot be parsed as filtering expressions.              |

### Basic of Falco Rules

#### Rule

A rule is a YAML object, part of the rules file, whose definition contains at least the following fields:

```yaml
- rule: shell_in_container
  desc: notice shell activity within a container
  condition: >
    evt.type = execve and 
    evt.dir = < and 
    container.id != host and 
    (proc.name = bash or
     proc.name = ksh)    
  output: >
    shell in a container
    (user=%user.name container_id=%container.id container_name=%container.name 
    shell=%proc.name parent=%proc.pname cmdline=%proc.cmdline)    
  priority: WARNING
```

- **Condition** is a Boolean predicate expressed using the condition syntax. It is possible to express conditions on all supported events using their respective supported fields.
- **Output** is a string that can use the same fields that conditions can use prepended by % to perform interpolation, akin to printf.
- **Priority** is similar to what we know as the severity of a syslog message. The priority is included in the message/JSON output/etc.

#### Macros

Macros provide a way to define common sub-portions of rules in a reusable way.

By looking at the condition above it looks like both evt.type = execve and evt.dir = < and container.id != host would be used many by other rules, so to make our job easier we can easily define macros for both:

```None
- macro: container
  condition: container.id != host
```

#### List

Lists are named collections of items that you can include in rules, macros, or even other lists.

Here are some example lists as well as a macro that uses them:

```None
- list: shell_binaries
  items: [bash, csh, ksh, sh, tcsh, zsh, dash]
```

### Defalut and Local Rule Files

Falco provides default rules, but you can add your own.

- The default falco rules file is installed at /etc/falco/falco_rules.yaml. It contains a predefined set of rules designed to provide good coverage in a variety of situations. The intent is that this rules file is not modified, and is replaced with each new software version.
- The local falco rules file is installed at /etc/falco/falco_rules.local.yaml. It is empty other than some comments. The intent is that additions/overrides/modifications to the main rules file are added to this local file. It will not be replaced with each new software version.

It can be found using `systemctl status falco`.  
