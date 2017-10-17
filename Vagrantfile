# Ubuntu+CakePHPを新規構築
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.synced_folder "cakephp", "/var/www/html/cakephp", create: "true"

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    # Apache
    apt-get install -y apache2
    apt-get install -y libapache2-mod-php7.0
    # PHP
    apt-get install -y php7.0 php7.0-intl php7.0-mbstring php7.0-xml
    # ZIP,UNZIP(Composerで使う)
    apt-get install -y zip unzip
    # Composer
    curl -s https://getcomposer.org/installer | php
    # CakePHPをインストール
    sudo -u ubuntu php composer.phar create-project --prefer-dist cakephp/app /vagrant/cakephp
    # Apache mod_rewrite設定
    a2enmod rewrite
    # AllowOverride All
    cp /vagrant/apache2.conf /etc/apache2/apache2.conf
    # 最後にApache再起動
    service apache2 restart
  SHELL
end
