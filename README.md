# roslaunch_remoto
Como rodar roslaunch sem acessar o ssh de outra maquina

O roslaunch usa extensão paramiko para criar conexão via ssh, e o paramiko não suporte extensões ecdsa, que e usado por padrão pela ultima atualização do ssh. Então ele não pode ler do arquivo known_hosts gerado com o ecdsa, assim, não consegue criar as conexões remotas.

Para fazer a conexão remota via roslaunch deve entrar em known_hosts:

$ nano ~/.ssh/known_hosts

Apagar tudo que esta no arquivo (por via de duvida, sempre faça um backup dos arquivos importantes que estão sendo alterados).
Apos apagar os arquivos faça a primeira conexão via ssh com este comando:

$ ssh -oHostKeyAlgorithms='ssh-rsa' host

Conecte-se normalmente e pronto. O roslaunch/paramiko-ssh entende o arquivo known_hosts e pode se conectar com a máquina remota.
