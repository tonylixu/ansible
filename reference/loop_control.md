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

### "label" directive:
When using complex data structures for looping the display might get a bit too “busy”, this is where the label directive comes to help:
```yaml
- name: create servers
  digital_ocean:
    name: "{{ item.name }}"
    state: present
  loop:
    - name: server1
      disks: 3gb
      ram: 15Gb
      network:
        nic01: 100Gb
        nic02: 10Gb
        ...
  loop_control:
    label: "{{ item.name }}"
```
This will now display just the label field instead of the whole structure per item, it defaults to {{ item }} to display things as usual.

### "pause" directive:
Another option to loop control is pause, which allows you to control the time (in seconds) between execution of items in a task loop.
```yaml
# main.yml
- name: create servers, pause 3s before creating next
  digital_ocean:
    name: "{{ item }}"
    state: present
  loop:
    - server1
    - server2
  loop_control:
    pause: 3
```
