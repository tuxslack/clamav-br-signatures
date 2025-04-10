# clamav-br-signatures

<p align="center">
  <img width="250" height="250" src="https://raw.githubusercontent.com/Cisco-Talos/clamav/main/logo.png" alt='Maeve, the ClamAV mascot'>
</p>


https://github.com/Cisco-Talos/clamav

## Adicionar novas assinaturas para ameaças mais recentes

Se você tem um arquivo que foi identificado como vírus por um antivírus do Windows (como o Windows Defender), e deseja adicionar uma assinatura para esse arquivo ao ClamAV.

ClamAV Signature Tool (sigtool)

O ClamAV vem com uma ferramenta chamada sigtool que pode ser usada para gerar assinaturas de arquivos em formatos diferentes, como hashes e expressões regulares. No entanto, o sigtool por si só não cria assinaturas automaticamente com base em uma análise completa de malware, mas é uma ferramenta útil para gerar assinaturas de arquivos conhecidos.


Gerar uma assinatura baseada em hash (SHA256, MD5 ou SHA1):

Se você tiver um arquivo específico que já foi identificado como malware e quer gerar uma assinatura baseada no hash, pode usar o sigtool da seguinte maneira:

sigtool --md5 /caminho/para/o/arquivo <br>
sigtool --sha1 /caminho/para/o/arquivo <br>
sigtool --sha256 /caminho/para/o/arquivo <br>

Isso irá gerar o hash correspondente do arquivo. Você pode usar esse hash para criar uma assinatura personalizada.

Ex:

Criando uma Assinatura Manualmente

sigtool --sha256 jogo.exe

2fc425b62f45c4ea04da32ae867f520192e515c4e145ab92590d27d36b7cb230:156:jogo.exe

Arquivo clamav-br-signatures.ndb

ee03285146c99a4cb042979566028503:151768:Trojan.GenericKD.61464077
025596c1433fdd0a8470a8f67bd022a2:88399:Phishing.HTML.Doc
f616866f79a438997916d0046ab82d8a:248367:Trojan.GenericKDS.61000948
c634bab45ecdefe5bfcbbc04d205f0e1:1245184:Trojan.GenericKD.61570137
dbf93d8a1fec0d65cadc3c9da5cb7ad4:214569:Trojan.NSIS.Guloader
2308f3613859e44ccad4f384bc5d3391:165201:Trojan.Zmutzy.Pong.2
cdc5b9c2a457856a1415bab1fad13860:190040:Trojan.GenericKD.61684063
57332083d1cef0b155eed1b2336a0d19:1245184:Trojan.Win32.Injector
c396e0d3b37a6db1b18e88ccbff3f167:841931:Trojan.GenericKD.61807796
9f0189b1ed95a5c5f7980f107f041a29:249370:Trojan.NSIS.Guloader
c0e9f2fc8507e4667b92b6970a23eeae:668484:Gen:Trojan.Olock.1



## Testar a Assinatura


Antes de adicionar a assinatura ao banco de dados do ClamAV, é importante testar se ela realmente detecta o malware corretamente sem gerar falsos positivos.

Você pode testar a assinatura manualmente usando o comando clamscan, apontando para o arquivo ou diretório onde o malware está localizado.

Para testar uma assinatura com um arquivo específico, use:

    clamscan --signatures=clamav-br-signatures.ndb /path/to/malware/sample

Onde clamav-br-signatures.ndb é o arquivo de banco de dados de assinaturas personalizado.

## Incluir novas assinaturas

O diretório de assinaturas padrão do ClamAV está localizado em:

$ cat /etc/clamd.conf | grep -i DatabaseDirectory | cut -d" " -f2

Coloque o arquivo de assinatura .ndb nesse diretório ou em um subdiretório apropriado.


## Atualize o banco de dados 

Depois de adicionar a assinatura, você precisa informar ao ClamAV para carregar o banco de dados atualizado.

freshclam

Nota: freshclam é utilizado normalmente para baixar as atualizações de assinatura do ClamAV a partir de um servidor remoto, mas ele também pode ser configurado para aceitar bancos de dados personalizados.


## Verificar a Detecção

Depois de adicionar a assinatura, você pode verificar se o ClamAV detecta corretamente o malware. Execute um escaneamento no diretório ou arquivo de teste e veja se a nova assinatura é acionada:

clamscan --infected --remove --log=/var/log/clamav_scan.log /caminho/do/diretorio

Este comando fará uma varredura em busca de malwares e removerá os infectados, caso seja configurado para tal, enquanto mantém o log das ações.



## Criação de assinaturas para o ClamAV usando IA (Inteligência Artificial) 

É possível criar assinaturas usando técnicas de aprendizado de máquina e IA para detectar padrões em arquivos maliciosos. Esse processo pode ser integrado ao ClamAV, mas exigiria ferramentas externas ou técnicas de análise que utilizam IA para gerar essas assinaturas.

Podemos usar técnicas de IA (como aprendizado de máquina e deep learning) para identificar e criar assinaturas para malwares. O processo envolve treinar um modelo de IA para identificar padrões maliciosos, gerar assinaturas e integrá-las ao ClamAV para detecção.






