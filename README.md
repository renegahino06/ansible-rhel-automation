# Ansible – Hardening baseline para RHEL 7, 8 y 9

Este repositorio contiene playbooks y roles de Ansible para aplicar un hardening **baseline** sobre servidores Red Hat Enterprise Linux 7, 8 y 9. El objetivo es mostrar buenas prácticas de automatización y seguridad, no reemplazar una auditoría formal CIS/STIG.

## Alcance

El rol `rhel_baseline` implementa, entre otros:

- Instalación de paquetes de seguridad básicos (`aide`, `chrony`, etc.).
- Eliminación de paquetes y servicios inseguros (por ejemplo `telnet`, `rsh`).
- Activación y refuerzo de `firewalld`.
- SELinux en modo `enforcing`.
- Hardening del servicio SSH (`sshd_config`).
- Ajustes básicos de `sysctl` para red.

Para perfiles de cumplimiento formales (CIS/Stig), existen roles específicos como:

- [`ansible-lockdown/RHEL9-CIS`](https://github.com/ansible-lockdown/RHEL9-CIS)
- [`RedHatOfficial.rhel8_cis` en Ansible Galaxy](https://galaxy.ansible.com/redhatofficial/rhel8_cis)

## Estructura del proyecto

```text
inventory/
  rhel7/
  rhel8/
  rhel9/
playbooks/
  hardening_rhel.yml
roles/
  rhel_baseline/
    tasks/
    handlers/
    defaults/
    vars/
```

## Requisitos

- Ansible 2.9+ (recomendado usar Ansible moderno).
- Acceso SSH a servidores RHEL 7, 8 o 9.
- Usuario con privilegios de sudo (configurado en el inventario).

Instalación de dependencias (si se usan roles externos):

```bash
ansible-galaxy install -r requirements.yml
```

## Uso

Ejemplo de ejecución sobre un servidor RHEL 8 definido en `inventory/rhel8/hosts`:

```bash
ansible-playbook -i inventory/rhel8/hosts playbooks/hardening_rhel.yml
```

Para RHEL 7:

```bash
ansible-playbook -i inventory/rhel7/hosts playbooks/hardening_rhel.yml
```

Y para RHEL 9:

```bash
ansible-playbook -i inventory/rhel9/hosts playbooks/hardening_rhel.yml
```

## Buenas prácticas y notas

- Este rol aplica cambios reales; pruébalo primero en entornos de laboratorio.
- Asegúrate de tener acceso de consola en caso de bloquearte por error en SSH o firewall.
- Puedes extender el rol con tareas adicionales basadas en guías oficiales de hardening RHEL y benchmarks CIS.