# Ansible module to install packages from AUR

## How to use

1. Copy `aur` file into `library/` directory of your Ansible project.
2. Use it in your task:
   ```yaml
   - name: install packages from aur
     become: yes
     aur:
       name: "{{ item }}"
       dest: "{{ home_dir }}/projects/ops/aur"
       username: "{{ my_username }}"
     with_items:
       - dmenu2
       - xrectsel
       - ffcast
     tags: aur
   ```

   Where:  
     `dest` is the path to where the AUR repositories will be cloned  
     `username` is the user who will have permissions for cloned aur repositories


## Dealing with mising GPG keys
Sometimes AUR packages require importing GPG keys. This is not something this
library handles. You will have to import the keys yourself before using the
module. The most straightforward way to do this is this:

```yaml
- name: retrieve gpg keys
  become: yes
  become_user: "{{ my_username }}"
  command: "gpg --keyserver {{ gpg_keyserver }} --recv-keys {{ item }}"
  with_items:
    - 1C61A2656FB57B7E4DE0F4C1FC918B335044912E # dropbox
    - 393587D97D86500B # python-wdllib
  tags: aur
```

