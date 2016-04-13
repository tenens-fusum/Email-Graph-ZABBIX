# Email_Graph_ZABBIX

Em caso de dúvida, sugestão ou dificuldade junte-se a nós no <b>Grupo do Telegram</b> <class="noteimportant"><a href="https://telegram.me/joinchat/B7JjiwivOYVKq5gPNDqFSA" class="wikilink2" title="Ingressar no Grupo" rel="nofollow">Gráfico no Email</a>.

Envio de itens alarmados no ZABBIX por email com gráficos.<br>
<!--O "How to" foi testado no ZABBIX 2.4 e no 3.0 e está baseado em Debian, caso não utilize Debian procure os pacotes descritos para sua distribuição. -->
O "How to" foi testado no ZABBIX 2.4 e no 3.0 com base em Debian.
<br>
<br>

#Requisitos:
<b>1 - </b>Ter o POSTFIX instalado e configurado, caso não tenha, <class="noteimportant"><a href="https://github.com/sansaoipb/Email_Gmail_ZABBIX" class="wikilink2" title="Instalar POSTFIX" rel="nofollow">Clique aqui</a>.


<b>2 -</b> Baixar os módulos <code>MIME::Lite</code> e <code>WWW::Mechanize</code>.
<br>
Ex:<br>
<blockquote> <p>CentOS 6.x e 7</p> </blockquote>
yum install perl-WWW-Mechanize perl-MIME-Lite
<blockquote> <p>Debian</p> </blockquote>
<pre>$ sudo apt-get install libmime-lite-perl libwww-mechanize-perl<br></pre>

<b>3 -</b> Adicione o arquivo <code>“email.pl“</code> na pasta de scripts do ZABBIX.<br>
Caso queira mudar a pasta padrão, edite a linha <code>“AlertScriptsPath=”</code> no <code>“zabbix_server.conf”</code> e aponte para uma de sua preferência.
<br>
<br>

#Edite os parâmetros:

<ul class="task-list">
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" checked="checked" disabled="disabled"><font><font class=""> “my $server_ip” = 'http://127.0.0.1/zabbix'</font></font></li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" checked="checked" disabled="disabled"><font><font class=""> “my $usuario”   = 'Admin';</font></font></li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" checked="checked" disabled="disabled"><font><font class=""> “my $senha”     = 'zabbix';</font></font></li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" checked="checked" disabled="disabled"><font><font class=""> “my $periodo”   = TEMPO_DO_GRÁFICO_EM_SEGUNDOS-(PADRÃO ESTÁ COM 1 HORA)</font></font></li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" checked="checked" disabled="disabled"><font><font class=""> “my $color”   = COR DO GRAFICO EM HEX. (SEM TRALHA), PADRÃO ESTÁ VERDE</font></font></li>
</ul>
<b>OBS:</b> O usuário que você declarar no campo <i>“my $usuario”</i> precisa ter permissão de no mínimo leitura no ambiente.<br><br>

<h3><a id="user-content-features" class="anchor" href="#features" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>Comando para teste</h3>

A estrutura do comando para realização de teste é: <b>Script, Email, Assunto, ID-do-Item#Nome-do-Item#CorpoDoEmail.</b><br>
Ex:<br>
<code>./email.pl SeuEmail@Provedor.com "Assunto" "123456#QualquerNome#CorpoDoEmail"</code><br>
<b>OBS:</b> ”123456” é um número fictício para exemplificar, busque uma ID válida em seu ambiente para realização do teste.<br><br>

#Configurando o envio

Com o script adicionado no local indicado acima, precisamos realizar algumas configurações no Front do ZABBIX, no <i>"Tipo de Mídia"</i>, (em Administração  > Tipo de Mídia) e a <i>"Ação"</i> (em Configuração  > Ações).

<h3><a id="user-content-features" class="anchor" href="#features" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>Tipo de Mídia</h3>
<blockquote> <p>Zabbix 2.4</p> </blockquote>
<img src="https://lh3.googleusercontent.com/-VShKQbvb-sI/VugV_Csop6I/AAAAAAAAHjA/pNAv2REt5h0RyuPqqDCSME-q9HS0cde5wCCo/s435-Ic42/Type.JPG"/><br><br>
<blockquote> <p>Zabbix 3.0</p> </blockquote>
<img src="https://lh3.googleusercontent.com/-fYsqsGPi_Ts/VwucDEi496I/AAAAAAAAIV8/PppgsqA6VlkJXdAgTTbZiS92FMOjCunWQCCo/s512-Ic42/Type_3.0.JPG"/><br><br>
<b>OBS:</b> Na versão 3.0, se faz obrigatório a utilização das macros <code> {ALERT.SENDTO}</code>, <code> {ALERT.SUBJECT}</code> e <code> {ALERT.MESSAGE}</code>, em caso de dúvidas, leia a Documentação 
<class="noteimportant"><a href="https://www.zabbix.com/documentation/3.0/manual/config/notifications/media/script" class="wikilink2" title="Documentação Oficial" rel="nofollow">Aqui</a>.<br><br>

<h3><a id="user-content-features" class="anchor" href="#features" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>Configurando o usuário</h3>

<img src="https://lh3.googleusercontent.com/-xyTMzbhq6Qk/VwuL3xQdSCI/AAAAAAAAIVk/MfcoKVOHv4o5nLGQ_AQTe1VXZyE5lcYagCCo/s428-Ic42/Media.JPG"/><br>

<h3><a id="user-content-features" class="anchor" href="#features" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>Criando a Ação:</h3>

A “<i>Mensagem Padrão</i>” na aba <b>“<u>Ação</u>”</b> está sendo executada no formato “HTML”, então você pode realizar a formatação que desejar, somente com uma “exigência”, a primeira linha deve permanecer com a macro <code> {ITEM.ID}#{ITEM.NAME}#</code> (<i>as variáveis de item <b>com # ao lado</b></i>)

Exemplificando sobre o HTML, abaixo começou com um parágrafo, e o {HOST.NAME} coloquei em negrito.
<br>
<br>

<h3><a id="user-content-features" class="anchor" href="#features" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>Imagem da Ação:</h3>

<img src="https://lh3.googleusercontent.com/-YDwRKvqPTZU/Vw28g-6OJPI/AAAAAAAAIZA/t2WRHtH1CqAsDmeRjPJMANv6Fhr6EP1sACCo/s438-Ic42/Action.JPG"/><br><br>

<!--
<img src="https://github.com/sansaoipb/Email-graph-ZABBIX/blob/master/Action.JPG"/><br><br>
-->

<h3><a id="user-content-features" class="anchor" href="#features" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" role="img" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1h-1c-1.5 0-3-1.69-3-3.5s1.55-3.5 3-3.5h4c1.45 0 3 1.69 3 3.5 0 1.41-0.91 2.72-2 3.25v-1.16c0.58-0.45 1-1.27 1-2.09 0-1.28-1.02-2.5-2-2.5H4c-0.98 0-2 1.22-2 2.5s1 2.5 2 2.5z m9-3h-1v1h1c1 0 2 1.22 2 2.5s-1.02 2.5-2 2.5H9c-0.98 0-2-1.22-2-2.5 0-0.83 0.42-1.64 1-2.09v-1.16c-1.09 0.53-2 1.84-2 3.25 0 1.81 1.55 3.5 3 3.5h4c1.45 0 3-1.69 3-3.5s-1.5-3.5-3-3.5z"></path></svg></a>Resultado:</h3>

<img src="https://lh3.googleusercontent.com/-fjIUckGXVFo/Vw6TyBlr9xI/AAAAAAAAIZU/LIw3qOz1hG8pl5Ek-sJbYVxyfeG9Q1hJACCo/s707-Ic42/ResultEmail.JPG"/>
<br>
<br>

#Conclusão

Este script é para agilizar a analise e ficar visualmente mais agradável o recebimento dos alarmes.
