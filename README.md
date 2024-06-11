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
