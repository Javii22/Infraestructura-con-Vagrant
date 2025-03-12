# Configuración de Infraestructura con Vagrant

## Descripción
 levantar una infraestructura de máquinas virtuales Debian sin entorno gráfico usando **Vagrant** y **VirtualBox**. 
 Se crearán 5 máquinas virtuales con una configuración optimizada para minimizar el consumo de recursos.

##  Vagrantfile
Este `Vagrantfile` genera **5 máquinas virtuales Debian**, cada una con **256MB de RAM y 1 núcleo de CPU**, además de una **IP estática** para evitar conflictos de DHCP.

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"

  (1..5).each do |i|
    config.vm.define "debian_vm#{i}" do |node|
      node.vm.hostname = "debian-vm#{i}"
      
      # Asignar IPs estáticas para evitar conflictos de DHCP
      node.vm.network "private_network", type: "static", ip: "192.168.56.1#{i}"

      node.vm.provider "virtualbox" do |vb|
        vb.memory = "256"  # 256MB de RAM
        vb.cpus = 1        # 1 núcleo de CPU
      end
    end
  end
end
```
## 🔹 Pasos para Usarlo

1. **Elimina cualquier máquina virtual anterior con:**
   ```powershell
   vagrant destroy -f
   ```

2. **Borra archivos temporales de Vagrant:**
   ```powershell
   rm -rf .vagrant
   ```

3. **Ejecuta para levantar las máquinas:**
   ```powershell
   vagrant up
   ```
