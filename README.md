# configurar-Apache-tomcat

Como instalar o Tomcat Server

A maneira mais fácil de instalar o Tomcat Server é pelo repositório de software padrão do Ubuntu. O repositório deve conter a versão estável mais recente do Tomcat.

    Primeiro, abra um terminal e faça o download das informações mais recentes do pacote com o seguinte comando:

    $ sudo apt update

    Em seguida, verifique o repositório para ver qual pacote do Tomcat está disponível para download:

    $ sudo apt-cache search tomcat

    Vemos na captura de tela abaixo que o tomcat9pacote é o que temos disponível para download.
    
    https://github.com/Oliveira4driano/configurar-Apache-tomcat/issues/1#issue-958311395
    
  Pesquisando no repositório de software Ubuntu para pacotes tomcat
Comece a baixar e instalar os pacotes tomcat9e tomcat9-admin(ou qualquer que seja o nome / versão atual dos pacotes no momento da leitura) e suas dependências com este comando:

$ sudo apt install tomcat9 tomcat9-admin

Após a instalação do Tomcat, ele deve iniciar automaticamente. Você pode verificar se está executando com o sscomando Você deve ver uma porta aberta, número 8080, pois essa é a porta padrão do Apache Tomcat.

$ ss -ltn
O comando ss indica que a porta 8080 está escutando conexões de entrada de qualquer origem

O Tomcat deve continuar a iniciar automaticamente quando o Ubuntu reiniciar. Você pode alterar esse comportamento a qualquer momento, desabilitando ou habilitando:

$ sudo systemctl enable tomcat9
OR
$ sudo systemctl disable tomcat9
Portas de firewall abertas para o Tomcat Server

Se o firewall UFW estiver em execução no seu sistema, os dispositivos externos terão problemas para se conectar ao servidor Tomcat. Digite o seguinte comando para permitir o tráfego TCP de entrada de qualquer origem para porta 8080:

$ sudo ufw allow from any to any port 8080 proto tcp

Teste o servidor Tomcat

Com o Tomcat em funcionamento, agora você deve acessá-lo em um navegador da web. Você pode conectar-se a ele através do endereço de loopback do seu sistema e especificando o número da porta do Tomcat:http://127.0.0.1:8080

O Apache Tomcat está em execução e pode ser conectado a partir de um navegador

Se você vir a mensagem "Funciona!" página, o Tomcat está acessível e funcionando corretamente.
Criar usuário para o Web Application Manager

Para acessar o gerenciador de aplicativos da web do Tomcat (o painel de configuração do administrador no Tomcat), precisamos configurar um novo usuário do Tomcat.

    Primeiro, use o nano ou o seu editor de texto preferido para abrir o tomcat-users.xmlarquivo. Observe que o nome do diretório para nós é "tomcat9", pois é a versão atual do Tomcat. O seu pode ser diferente.

    $ sudo nano /etc/tomcat9/tomcat-users.xml
    
Dentro deste arquivo, cole as três linhas a seguir acima da tag. Isso criará um novo usuário chamado tomcatcom uma senha de pass. Substitua seus próprios valores lá.

Editando o arquivo XML tomcat-users com credenciais do usuário para acessar a GUI do administrador
Salve e feche o arquivo e reinicie o Tomcat Server:

$ sudo systemctl restart tomcat9

Acesse o Tomcat Web Application Manager

    Navegue para http://127.0.0.1:8080/manager/htmlacessar o Tomcat Web Application Manager. Você deve ser solicitado pelas credenciais que acabamos de configurar.
    
    Depois de fazer o login com as credenciais, você deverá receber a página principal do Tomcat Web Application Manager.
        Conexão bem-sucedida ao Tomcat Web Applcation Manager

Já terminamos. De dentro deste painel de administração, você poderá definir hosts virtuais e outras configurações.
Conclusão

Implantando o Apache Tomcat no Ubuntu 20.04 O Focal Fossa é uma ótima maneira de hospedar seu servidor web Java HTTP. Os administradores do site o usam para executar Java Servlets, JavaServer Pages e Java Expression Language. A configuração do Tomcat no Ubuntu é relativamente fácil e o pacote admin amplia sua funcionalidade, fornecendo uma interface da web fácil para gerenciar a configuração do servidor.

https://goto-linux.com/pt/2020/6/4/instalacao-do-ubuntu-20.04-tomcat/



    
