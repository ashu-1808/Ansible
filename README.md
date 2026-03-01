# Ansible
---

## 1️⃣ What is ?

Ansible is an open-source automation tool used for:
1. Configuration Management
2. Application Deployment
3. Provisioning
4. Orchestration

It is developed by Red Hat.
### ✅ Key Features
1. Agentless (No agent needed on target servers)
2. Uses SSH for Linux, WinRM for Windows
3. YAML based (Easy to read)
4. Idempotent (Runs multiple times safely)

---

# 2️⃣ Ansible Architecture

![Image](https://miro.medium.com/0%2ASr1T30hc8WT269jV)

![Image](https://miro.medium.com/v2/da%3Atrue/resize%3Afit%3A1200/0%2AsMSfIbPO8mH299to)

![Image](https://miro.medium.com/1%2A8H4XYCNV-xamG0joz22apQ.png)

![Image](https://images.tekanaid.com/terraform-vs-ansible-learn-the-differences-ansible-agentless.png)

### 🔹 Components
| Component     | Explanation                       |
| ------------- | --------------------------------- |
| Control Node  | Where Ansible is installed        |
| Managed Nodes | Target servers                    |
| Inventory     | List of servers                   |
| Modules       | Small programs that perform tasks |
| Playbook      | YAML file containing tasks        |

---

# 3️⃣ Installation (Ubuntu)
```bash
sudo apt update
sudo apt install ansible -y
ansible --version
```

---

# 4️⃣ Inventory File
### Static Inventory Example:

```ini
[web]
192.168.1.10
192.168.1.11

[db]
192.168.1.20
```

### Check connectivity:
```bash
ansible all -m ping
```

---

# 5️⃣ Ad-Hoc Commands
Used for quick tasks.

```bash
ansible all -m ping
ansible web -m shell -a "uptime"
ansible all -m apt -a "name=nginx state=present" --become
```

---

# 6️⃣ Playbooks (YAML)
### Basic Playbook Example:
```yaml
---
- name: Install nginx
  hosts: web
  become: yes

  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
```

Run:

```bash
ansible-playbook install.yml
```

---

# 7️⃣ Important Modules (Interview Focus)

| Module    | Use                  |
| --------- | -------------------- |
| ping      | Test connectivity    |
| apt / yum | Package installation |
| service   | Start/stop service   |
| copy      | Copy files           |
| file      | Create directory     |
| user      | Create users         |
| git       | Clone repo           |

---

# 8️⃣ Variables
### Playbook Variables

```yaml
vars:
  package_name: nginx
```

### Inventory Variables

```ini
[web]
192.168.1.10 ansible_user=ubuntu
```

---

# 9️⃣ Handlers

Used to restart services only when changes occur.
```yaml
tasks:
  - name: Install nginx
    apt:
      name: nginx
      state: present
    notify: restart nginx

handlers:
  - name: restart nginx
    service:
      name: nginx
      state: restarted
```

---

# 🔟 Ansible Roles (Very Important for Jobs)

![Image](https://miro.medium.com/0%2AjDQx0eCwsvaBKivi)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1200/1%2AxJvuzzALm5ZbM-LCSHDyJg.png)

![Image](https://ansible-dims-playbooks.readthedocs.io/en/latest/_images/ansible-overview.png)

### Role Structure:
```
roles/
  nginx/
    tasks/
    handlers/
    vars/
    defaults/
    templates/
    files/
```

### Why Roles?
* Reusability
* Clean structure
* Scalable automation
---

# 1️⃣1️⃣ Ansible Vault (Security)
Used to encrypt sensitive data.
```bash
ansible-vault create secrets.yml
ansible-vault edit secrets.yml
ansible-playbook site.yml --ask-vault-pass
```

---

# 1️⃣2️⃣ Templates (Jinja2)
Used for dynamic configuration files.
Example:

```jinja2
server_name {{ inventory_hostname }};
```

---

# 1️⃣3️⃣ Ansible vs Other Tools
| Feature        | Ansible | Chef  | Puppet |
| -------------- | ------- | ----- | ------ |
| Agent Required | ❌ No    | ✅ Yes | ✅ Yes  |
| Language       | YAML    | Ruby  | Ruby   |
| Push/Pull      | Push    | Pull  | Pull   |

---

# 1️⃣4️⃣ Real-Time DevOps Use Cases
Since you're preparing for DevOps interviews:
✅ Install & configure Nginx on 20 servers
✅ Deploy Docker containers
✅ CI/CD integration
✅ Patch management
✅ User creation across servers

---

# 1️⃣5️⃣ Important Interview Questions
1. What is idempotency?
2. Difference between Playbook and Role?
3. What is Ansible Vault?
4. How does Ansible connect to nodes?
5. What is handler?
6. What is inventory?

---

# 🔥 What You Should Add To Be Job Ready
Since you're aiming for DevOps roles, also learn:
* Ansible with AWS (EC2 provisioning)
* Dynamic Inventory
* Ansible + Docker
* Ansible in CI/CD (Jenkins)
* Error handling (`ignore_errors`, `when`, `tags`)

---

