# Fedora Local Playbook

Ansible playbook to automate the setup of local environment using Fedora.

## Using WSL

1. **Prepare Fedora Container Base:**
   - Download the Fedora Container Base image from [Fedora](https://kojipkgs.fedoraproject.org//packages/Fedora-Container-Base/).
   - Unpack the `Fedora-Container-Base-*.x86_64.tar.xz` file.
   - Locate the rootfs in `layer.tar`.

2. **Create a Folder for WSL Distro:**
   ```
   mkdir $HOME\wsl\fedora
   ```

3. **Install the Distro:**
   ```
   wsl --import fedora $HOME\wsl\fedora $HOME\Downloads\layer.tar
   ```

## Setting Up a New User

1. **Install Necessary Packages Absent in Container Base:**
   ```
   sudo dnf install upgrade -y
   dnf install passwd -y
   dnf install util-linux-user -y
   dnf install cracklib-dicts -y
   ```

2. **Add a New User and Set Password:**
   ```
   useradd -m $username
   sudo usermod -aG wheel $username
   passwd $username
   ```

3. **Get the Playbook:**
   ```
   ## Installation of Ansible and Git
   sudo dnf install ansible -y
   sudo dnf install git -y

   ## Clone the Ansible Configuration
   git clone https://github.com/ncarchar/.ansible.git
   ```

## Run the Playbook

Execute the playbook:

```
ansible-playbook local.yml -K --ask-vault-pass
```

## Additional Steps

- After the playbook execution, make sure to source the copied `.bashrc`.
- Update .ansible repository to use ssh now that it is configured.
