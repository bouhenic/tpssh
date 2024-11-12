Vagrant.configure("2") do |config|
  # Configuration de la première VM : Alice
  config.vm.define "alice" do |alice|
    alice.vm.box = "ubuntu/bionic64" # ou "ubuntu/focal64" pour Ubuntu 20.04
    alice.vm.hostname = "alice"
    alice.vm.network "private_network", ip: "192.168.56.10"

    alice.vm.provision "shell", inline: <<-SHELL
      # Installation d'OpenSSH Server
      sudo apt-get update
      sudo apt-get install -y openssh-server

      # Création de l'utilisateur 'alice' avec mot de passe 'alice'
      sudo useradd -m -s /bin/bash alice
      echo 'alice:alice' | sudo chpasswd

      # Activer l'authentification par mot de passe pour SSH
      sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
      sudo systemctl restart ssh

      # Préconfigurer la réponse pour éviter le blocage lors de l'installation de Wireshark
      echo "wireshark-common wireshark-common/install-setuid boolean false" | sudo debconf-set-selections

      # Installer Wireshark, Firefox et Ettercap
      sudo apt-get install -y wireshark xauth x11-apps

      # Ajouter la variable DISPLAY dans le fichier .bashrc pour qu'elle soit disponible à chaque session
      echo "export DISPLAY=localhost:10.0" >> /home/bob/.bashrc

      # Créer le groupe 'wireshark' si non existant
      sudo groupadd wireshark || true

      # Ajouter l'utilisateur 'bob' au groupe 'wireshark'
      sudo usermod -aG wireshark alice
    SHELL
  end

  # Configuration de la deuxième VM : Bob
  config.vm.define "bob" do |bob|
    bob.vm.box = "ubuntu/bionic64" # ou "ubuntu/focal64" pour Ubuntu 20.04
    bob.vm.hostname = "bob"
    bob.vm.network "private_network", ip: "192.168.56.11"

    bob.vm.provision "shell", inline: <<-SHELL
      # Installation d'OpenSSH Server
      sudo apt-get update
      sudo apt-get install -y openssh-server

      # Création de l'utilisateur 'bob' avec mot de passe 'bob'
      sudo useradd -m -s /bin/bash bob
      echo 'bob:bob' | sudo chpasswd

      # Activer l'authentification par mot de passe pour SSH
      sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
      sudo systemctl restart ssh

      # Préconfigurer la réponse pour éviter le blocage lors de l'installation de Wireshark
      echo "wireshark-common wireshark-common/install-setuid boolean false" | sudo debconf-set-selections

      # Installer Wireshark, Firefox et Ettercap
      sudo apt-get install -y wireshark xauth x11-apps

      # Ajouter la variable DISPLAY dans le fichier .bashrc pour qu'elle soit disponible à chaque session
      echo "export DISPLAY=localhost:10.0" >> /home/bob/.bashrc

      # Créer le groupe 'wireshark' si non existant
      sudo groupadd wireshark || true

      # Ajouter l'utilisateur 'bob' au groupe 'wireshark'
      sudo usermod -aG wireshark bob
    SHELL
  end

  # Configuration de la troisième VM : Eve
  config.vm.define "eve" do |eve|
    eve.vm.box = "debian/buster64"
    eve.vm.hostname = "eve"
    eve.vm.network "private_network", ip: "192.168.56.12"

    eve.vm.provision "shell", inline: <<-SHELL
      # Installation d'OpenSSH Server
      sudo apt-get update
      sudo apt-get install -y openssh-server

      # Création de l'utilisateur 'eve' avec mot de passe 'eve'
      sudo useradd -m -s /bin/bash eve
      echo 'eve:eve' | sudo chpasswd

      # Activer l'authentification par mot de passe pour SSH
      sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
      sudo systemctl restart ssh
    SHELL
  end
end
