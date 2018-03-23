## loop_control
loop_control adds the ability to loop over the set of tasks in one shot. Ansible by default sets the loop variable `item` for each loop, which causes these nested loops to overwrite the value of `item` from the "outer" loops. As of Ansible 2.1+ the `loop_contorl` option can be used to specify the name of the variable to be used for the loop.

### Examples:
```yaml
# main.yml
- include: inner.yml
- include_tasks: inner.yml
  loop:
    - 1
    - 2
    - 3
  loop_control:
    loop_var: outer_item

# inner.yml
- debug:
    msg: "outer item={{ outer_item }} inner item={{ item }}"
  loop:
    - a
    - b
    - c
```
In this exmaple, in the output messages, `item` will be `1, 2, 3`, and the `outer_item` will be `a, b, c`.
