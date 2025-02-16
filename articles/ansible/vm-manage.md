---
title: Manage Linux virtual machines in Azure using Ansible 
description: Learn how to manage a Linux virtual machine in Azure using Ansible
keywords: ansible, azure, devops, bash, cloudshell, playbook, bash
ms.topic: tutorial
ms.date: 08/28/2021
ms.custom: devx-track-ansible
---

# Manage Linux virtual machines in Azure using Ansible

Ansible allows you to automate the deployment and configuration of resources in your environment. In this article, you use an Ansible playbook to start and stop a Linux virtual machine. 

## Prerequisites

[!INCLUDE [open-source-devops-prereqs-azure-sub.md](../includes/open-source-devops-prereqs-azure-subscription.md)]
[!INCLUDE [ansible-prereqs-cloudshell-use-or-vm-creation2.md](includes/ansible-prereqs-cloudshell-use-or-vm-creation2.md)]

## Stop a virtual machine

In this section, you use Ansible to deallocate (stop) an Azure virtual machine.

1. Sign in to the [Azure portal](https://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Open [Cloud Shell](/azure/cloud-shell/overview).

1. Create a file named `azure-vm-stop.yml`, and open it in the editor:

    ```bash
    code azure-vm-stop.yml
    ```

1. Paste the following sample code into the editor:

    ```yaml
    - name: Stop Azure VM
      hosts: localhost
      connection: local
      tasks:
        - name: Stop virtual machine
          azure_rm_virtualmachine:
            resource_group: {{ resource_group_name }}
            name: {{ vm_name }}
            allocated: no
    ```

1. Replace the `{{ resource_group_name }}` and `{{ vm_name }}` placeholders with your values.

1. Save the file and exit the editor.

1. Run the playbook using [ansible-playbook](https://docs.ansible.com/ansible/latest/cli/ansible-playbook.html)

    ```bash
    ansible-playbook azure-vm-stop.yml
    ```

1. After running the playbook, you see output similar to the following results:

    ```bash
    PLAY [Stop Azure VM] ********************************************************

    TASK [Gathering Facts] ******************************************************
    ok: [localhost]

    TASK [Deallocate the Virtual Machine] ***************************************
    changed: [localhost]

    PLAY RECAP ******************************************************************
    localhost                  : ok=2    changed=1    unreachable=0    failed=0
    ```

## Start a virtual machine

In this section, you use Ansible to start a deallocated (stopped) Azure virtual machine.

1. Sign in to the [Azure portal](https://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Open [Cloud Shell](/azure/cloud-shell/overview).

1. Create a file named `azure-vm-start.yml`, and open it in the editor:

    ```bash
    code azure-vm-start.yml
    ```

1. Paste the following sample code into the editor:

    ```yaml
    - name: Start Azure VM
      hosts: localhost
      connection: local
      tasks:
        - name: Start virtual machine
          azure_rm_virtualmachine:
            resource_group: {{ resource_group_name }}
            name: {{ vm_name }}
    ```

1. Replace the `{{ resource_group_name }}` and `{{ vm_name }}` placeholders with your values.

1. Save the file and exit the editor.

1. Run the playbook using [ansible-playbook](https://docs.ansible.com/ansible/latest/cli/ansible-playbook.html)

    ```bash
    ansible-playbook azure-vm-start.yml
    ```

1. After running the playbook, you see output similar to the following results:

    ```bash
    PLAY [Start Azure VM] ********************************************************

    TASK [Gathering Facts] ******************************************************
    ok: [localhost]

    TASK [Start the Virtual Machine] ********************************************
    changed: [localhost]

    PLAY RECAP ******************************************************************
    localhost                  : ok=2    changed=1    unreachable=0    failed=0
    ```

## Next steps

> [!div class="nextstepaction"] 
> [Tutorial: Manage Azure dynamic inventories using Ansible](./dynamic-inventory-configure.md)