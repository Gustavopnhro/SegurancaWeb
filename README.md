# ☠️ Entendendo e mapeando ameaças 

## 🗒️ Descrição 
Esse markdown foi criado com o objetivo de orientar às boas práticas para ter uma aplicação web livre de algumas das vulnerabilidades mais conhecidas.

🚨 Aviso: Este markdown foi construído a partir do curso "Aprenda Ethical Hacking em Sites e Aplicações Web de forma prática..." ministrado pelo instrutor Samuel Gonçalves Pereira

### 🎯 Seção um - Vulnerabilidades 
As vulnerabilidades são pontos onde a sua aplicação está exposta como um pequeno furo no que deveria ser uma grande armadura de metal.

Vamos mapear algumas das principais vulnerabilidades que podem haver em uma aplicação web e suas implicações:

##### SQL INJECTION
Como o nome sugere é uma injeção de <b>SQL</b>, para os menos familiarizados com o nome SQL, é a linguagem manipular informações/dados armazenados em um banco de dados.

###### 👀 Como aparece?
A injeção de SQL aparece em campos como login, senha  e qualquer outro campo que pressuponha uma consulta em um banco de dados para alguma validação.

###### 🤔 Por que ele ocorre? 

Uma SQL injection ocorre quando um atacante encontra vulnerabilidades nas práticas de segurança e permite que os campos interajam diretamente com o banco de dados usando SQL. Em mãos dessa vulnerabilidade o hacker consegue executar códigos SQL em campos que estão com essa falha assim conseguindo acessos indevidos ou até mesmo conseguir todos os dados existentes no banco de dados exatamente pela ausência da sanitização (tratamento) dos dados antes de ir para o banco de dados.

###### 🔍 Ferramentas para teste
Aqui vai algumas ferramentas para testar SQL injection:
- [OWASP ZAP](https://www.zaproxy.org/download/) (Zed Attack Proxy) - Utlizado para fins de captura de Cookies e Nível de segurança;
- SQLMAP - Nativo do próprio Kali Linux - Utilizado para fazer uma varredura nas vulnerabilidades dos campos de forma automatizada;

##### XSS SCRIPT
<b>XSS Script</b> ou <b>Cross-Site Scripting</b> consiste na execução de comandos javascript dentro de algum campo que não esteja devidamente tratado, isso implica em algo semelhante ao SQL Injection com a diferença de que permite a inclusão da tag <b>"script"</b> do HTML.

Mas não somente, como mostrado no módulo de teste é possível também ter acesso às sessões das vítimas e direcionar scripts específicos que podem simular um login de alguma página e então atuar também como um capturador de senhas. 
###### 👀 Como aparece?
O <b>XSS Script</b> pode ocorrer de diversas formas, uma delas é havendo um campo qualquer que permita escrever algo, e então o script poderia ser injetado através deste campo

###### 🤔 Por que ele ocorre? 
Como na maioria dos citados esta vulnerabilidade também está atrelada à falta de sanitização dos textos escritos permitindo que tags sejam inseridas de forma indiscriminadas assim gerando esse calcanhar de Aquiles no sistema.
###### 🔍 Ferramentas para teste
- [Beef](https://beefproject.com/) - Programa que permite a criação de um servidor local para a hospedagem do malware e então é possível direcionar o script injetado para este servidor local dando acesso ao sistema.

##### COMMAND INJECTION

###### 👀 Como aparece?
Ele aparece a partir da vulnerabilidade que permitam que o atacante tenha acesso aos diretórios e arquivos de um servidor que no exemplo em questão está exposto ao permitir o uso do comando "nslookup" este que é nativo tanto do Windows quanto do Linux permitindo através da consulta do servidor de DNS retornar o endereço ip que está relacionado àquele site.

###### 🤔 Por que ele ocorre? 
Como os dois últimos o command injection também aproveita-se da vulnerabilidade criada pela falta de sanitização de caracteres ao serem enviados em campos de envio, permitindo que comandos cheguem nesse caso ao terminal do servidor sem ao menos passarem pelo processo de sanitização de caracteres, entendemos então que, através da sanitização de caracteres já teríamos sanado pelo menos essas três vulnerabilidades

###### 🔍 Ferramentas para teste
- [Commix](https://github.com/commixproject/commix) - O programa é nativo do Kali Linux mas também há o repositório para fins de leitura da documentação.

🚨 Aviso: No caso do teste foi utilizado o Commix + [OWASP ZAP](https://www.zaproxy.org/download/) para capturar o cookie da sessão.

##### LFI/RFI
- LFI (Local File Injection)
De forma bem resumida se trata da injeção de arquivos locais (existentes na sua máquina) para o servidor de forma indiscriminada, permitindo que possa ser enviado até mesmo um arquivo malicoso.

- RMI (Remote File Injection)
Reiterando o conceito acima a diferença para o RMI é que conseguimos implantar ou injetar arquivos remotos no servidor através de algum portão de depedências que consiga ser referenciada através da página

###### 👀 Como aparece?
Normalmente é comum que esses tipos de vulnerabilidades sejam encontradas em páginas que contenham a aba de upload de arquivos, fotos, documentos e etc.

###### 🤔 Por que ele ocorre? 
Ocorre também através da vulnerabilidade de sanitização, mas dessa vez de arquivos, extensões, verificação de código maliciosos e principalmente da falta de isolamento do local onde o arquivo será inserido do resto do servidor

###### 🔍 Ferramentas para teste

- C99shell.php (Backdoor)
- MiniShell.php (Backdoor)

##### BRUTE FORCE
Brute force ou força bruta é o tipo de ataque que visa através de uma série de palavras-chaves e usuários fazer massivas tentativas de acessar alguma conta até que ela seja encontrada.

###### 👀 Como aparece?
O Brute force não precede a existência de alguma falha muito brusca, pois pode ser realizada em sites protegidos com a diferença de que, em sites não protegidos esse ataque tem sua eficácia e em locais protegidos ele é barrado logo no início não permitindo seu avanço.

###### 🤔 Por que ele ocorre? 
Não há uma razão específica para o Brute Force ocorrer, basta ter algum campo que permita login e tcharam, pode ocorrer um brute force, entretanto como citado acima podemos instaurar limites de tentativas às nossas aplicações web visando barrar o potencial desse ataque.

###### 🔍 Ferramentas para teste
- [CEWL](https://www.100security.com.br/cewl) - Nativo do Kali Linux e permite a criação de suas próprias "wordlists"
- [Hydra](https://acaditi.com.br/hydra-ferramenta-de-brute-force-para-testes-de-seguranca/) - Ataques de Brute Force com wordlists 
- [OWASP ZAP](https://www.zaproxy.org/download/) - Ataques de Brute Force com wordlists

##### DoS (Denial of Service) 
Denial of Service ou Negação de serviço é um ataque baseado em requisições feitas de forma massiva em direção ao servidor visando sobrecarregá-lo e por fim tirar o serviço do ar.

###### 👀 Como aparece?
Não é necessário um ambiente específico para que ele ocorra, basta que o servidor aceite requisições e esteja online ao público.
###### 🤔 Por que ele ocorre? 
Também nao há uma razão específica para que este ataque ocorra, mas há formas de se defender dele atráves de algumas soluções digitais que tem uma "blacklist" de ip's que geralmente são utilizados para ataques desse gênero.

###### 🔍 Ferramentas para teste

Hping - Ferramenta nativa no Kali Linux


### Seção dois - Trânsito Seguro 🔰
O trânsito seguro de informações é tudo o que tange a criptografia na comunicação entre duas partes, não é incomum ver em alguns sites o <b>certificado de SSL/TLS</b> que garante que a conexão com o site é feita de forma criptografada

##### Mas então como seria uma comunicação não-criptografada?
Uma comunicação <b>não-criptografada</b> é onde os dados tantos de requisição quanto dos métodos ficam expostos para "sniffers" ou farejadores que conseguem ler essas requisições e trazer para algum atacante que tenha interesse nessas informações.

##### E uma comunicação segura? Como é feita?
Uma comunicação segura pautada nas certificações SSL/TLS não permite que os pacotes sejam identificados em meio a rede, e se permitirem nenhuma informação muito sensível será possível de ser reconhecida por algum atacante garantindo assim um tráfego seguro.

### Seção três - Defesa 🛡️

Agora chegamos ao <i>"Magnus Opus"</i> como nós conseguimos garantir que a nossa aplicação web não está vulnerável a estes principais tipos de ataque?
Há diversas formas de fazer essa abordagem mas neste markdown vamos abordar o ethical hacking que foi utilizado no curso.

##### Mas então, eu vou fazer todos os teste? 
Não é necessário, através de programas voltados para a auditoria de sistemas no que tange segurança nós podemos fazer todos esses testes de vulnerabilidades para saber onde a nossa aplicação precisa de melhora, entre eles podemos citar:

- [NIKTO](https://github.com/sullo/nikto)
- [WPSCAN](https://wpscan.com/) 
- [OWASP ZAP](https://www.zaproxy.org/download/)
- [GoLismero](https://github.com/golismero/golismero)
- [WAPITI](https://github.com/wapiti-scanner/wapiti)

Todos esses softwares permitem o scanning de vulnerabilidades no site dando assim um maior direcionamento para as soluções para além até das vulnerabilidades que apareceram neste post.

Caso você faça utilização de <i>nginx</i> ou <i>apache</i> para dar vida a sua aplicação é possível também utilizar o [ModSecurity](https://github.com/SpiderLabs/ModSecurity.git) que traz uma espécie de <b>Firewall</b> para as comunicações realizadas pela sua aplicação, ou sendo ainda mais específico uma <b>WAF (Web Application Firewall) </b> que faz um filtro e investigação dos pacotes antes de permitir que eles entrem no servidor.

E com isso encerramos o nosso manual de boas práticas para a construção de uma aplicação web mais segura, e com isso eu encerro por aqui! Até a próxima!

<img src="https://www.google.com/url?sa=i&url=https%3A%2F%2Ftenor.com%2Fsearch%2Fmike-cena-stickers&psig=AOvVaw1Y64qm62hGF38gYjsn_qr7&ust=1703612697490000&source=images&cd=vfe&opi=89978449&ved=0CBEQjRxqFwoTCICumv-Rq4MDFQAAAAAdAAAAABAP" alt="John Cena dancing">
