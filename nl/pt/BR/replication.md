---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Trabalhando com replicação

A replicação usa um de seus planejamentos de captura instantânea para copiar automaticamente capturas instantâneas para um volume de destino em um data center remoto. As cópias podem ser recuperadas no site remoto se um evento catastrófico ou distorção de dados ocorre.

Com réplicas, é possível:

- Recuperar de falhas do site e outros desastres rapidamente efetuando failover para o volume de destino.
- Efetuar failover para um momento específico na cópia de DR.

Antes de replicar, deve-se criar um planejamento de captura instantânea. Ao efetuar failover, você está "invertendo o comutador" do volume de armazenamento em seu data center primário para o volume de destino em seu data center remoto. Por exemplo, seu data center primário é Londres e seu data center secundário é Amsterdã. Se um evento de falha ocorresse, você efetuaria failover para Amsterdã, conectando-se ao volume agora primário de uma instância de cálculo em Amsterdã. Depois que seu volume em Londres é reparado, uma captura instantânea é tomada do volume de Amsterdã para efetuar failback para Londres e para o volume novamente primário de uma instância de cálculo em Londres.


## Como determinar o data center remoto para meu volume de armazenamento replicado?

Os data centers do {{site.data.keyword.BluSoftlayer_full}} são emparelhados em combinações primárias e remotas no mundo todo.
Veja a Tabela 1 para a lista completa de disponibilidade de data center e destinos de replicação.


<table style="width: 80.0%;">
	<caption style="text-align: left;"><p>Tabela 1 - Esta tabela mostra a lista completa de data centers com recursos aprimorados em cada região. Cada região é uma coluna separada. Algumas cidades, como Dallas, San Jose, Washington DC, Amsterdã, Frankfurt, Londres e Sydney, têm múltiplos data centers.</p>
		<p>&#42; Os data centers na região EUA 1 NÃO têm armazenamento aprimorado. Os hosts em data centers com recursos de armazenamento aprimorados <strong>não podem</strong> iniciar a replicação com destinos de réplica em data centers dos EUA 1.</p>
</caption>
	<thead>
		<tr>
			<th>EUA 1 &#42;</th>
			<th>EUA 2</th>
			<th>América Latina</th>
			<th>Canadá</th>
			<th>Europa</th>
			<th>Ásia-Pacífico</th>
			<th>Austrália</t>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>DAL01<br />
				DAL05<br />
				DAL06<br />
				HOU02<br />
				SJC01<br />
				WDC01<br />
				<br />
				<br />
				<br />
				<br />
				<br />
			</td>
			<td>SJC03<br />
			       SJC04<br />
			       WDC04<br />
			       WDC06<br />
			       WDC07<br />
			       DAL09<br />
				DAL10<br />
				DAL12<br />
				DAL13<br />
				<br /><br />
			</td>
			<td>MEX01<br />
				SAO01<br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
			</td>
			<td>TOR01<br />
				MON01<br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
			</td>
			<td>
				AMS01<br />
				AMS03<br />
				FRA02<br />
				FRA04<br />
				FRA05<br />
				LON02<br />
				LON04<br />
				LON06<br />
				OSL01<br />
				PAR01<br />
				MIL01<br />
			</td>
			<td>HKG02<br />
				TOK02<br />
				SNG01<br />
				SEO01<br />
                                CHE01<br />
				<br />
				<br />
				<br />
				<br />
				<br />
				<br />
			</td>
			<td>
				SYD01<br />
				SYD04<br />
				MEL01<br />
				<br /><br /><br /><br /><br /><br /><br /><br />
			</td>
		</tr>
	</tbody>
</table>


## Como criar uma replicação inicial?

As replicações trabalham fora de um planejamento de captura instantânea. Deve-se primeiro ter um espaço de captura instantânea e um planejamento de captura instantânea configurado para o volume de origem antes de poder replicar. Você receberá prompts que permitem que saiba o espaço que precisa ser comprado ou um planejamento configurado se tentar configurar a replicação e um ou outro não estiver no local. As replicações são gerenciadas em **Armazenamento** > **{{site.data.keyword.filestorage_short}}** no [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window}.

1. Clique em seu volume de armazenamento.
2. Clique na guia **Réplica** e clique no link **Comprar uma replicação**.
3. Selecione um planejamento de captura instantânea existente que você deseja que suas replicações sigam. A lista contém todos os seus planejamentos de captura instantânea ativa.
  **Nota:** será possível selecionar somente um planejamento, mesmo se você tiver uma combinação de por hora, diário ou semanal.  Todas as capturas instantâneas capturadas desde o ciclo de replicação prévio serão replicadas independentemente do planejamento que as originou.
4. Clique na seta suspensa **Local** e selecione o data center que será o seu site de DR.
5. Clique em **Continuar**.
6. Insira um **Código promocional** se você tiver um e clique em **Recalcular**. Os outros campos na caixa de diálogo serão padronizados.
7. Clique na caixa de seleção **Eu li o contrato de prestação de serviços principal…** e clique em **Fazer pedido**.


## Como editar uma replicação existente?

É possível editar seu planejamento de replicação e mudar o seu espaço de replicação na guia **Primário** ou **Réplica** em **Armazenamento** > **{{site.data.keyword.filestorage_short}}** no [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window}.


## Como editar um planejamento de replicação?

Na realidade, você está mudando um planejamento de captura instantânea porque seu planejamento de replicação é baseado em um planejamento de captura instantânea existente. Para mudar o planejamento de réplica, por exemplo, de Por hora para Semanal, deve-se cancelar o planejamento de replicação e configurar um novo.

A mudança do planejamento pode ser feita na guia **Primário** ou **Réplica**.

1. Clique no menu **Ações** da guia **Primário** ou **Réplica**.
2. Selecione **Editar planejamento de captura instantânea**.
3. Consulte o quadro Captura instantânea em Planejamento para determinar qual planejamento você está usando para replicação. Faça as mudanças no planejamento que está sendo usado para replicação. Por exemplo, se o seu planejamento de replicação é **Diário**, é possível mudar o horário do dia em que a replicação deve ocorrer.
4. Clique em **Salvar**.


## Como mudar o espaço de replicação?

Seu espaço de captura instantânea primário e seu espaço de réplica devem ser iguais. Se você mudar o espaço na guia **Primário** ou **Réplica**, ele incluirá espaço automaticamente nos data centers de origem e de destino. Esteja ciente de que aumentar o espaço de captura instantânea acionará uma atualização de replicação imediata.

1. Clique no menu **Ações** da guia **Primário** ou **Réplica**.
2. Selecione **Incluir mais espaço de captura instantânea**.
3. Selecione o tamanho do armazenamento e clique em **Continuar**.
4. Insira um **Código promocional** se você tiver um e clique em **Recalcular**. Os outros campos na caixa de diálogo serão padronizados.
5. Clique na caixa de seleção **Eu li o contrato de prestação de serviços principal…** e clique em **Fazer pedido**.


## Como ver meus volumes de réplica na Lista de volumes?

É possível visualizar seus volumes de replicação na página {{site.data.keyword.filestorage_short}} em **Armazenamento** > **{{site.data.keyword.filestorage_short}}**. O Nome do volume tem o nome do volume primário seguido por REP. O Tipo é Endurance (Performance) – Réplica. O Endereço de destino é N/D porque o volume de réplica não está montado no data center de réplica e o Status é Inativo.



## Como visualizar detalhes de um volume replicado no data center de réplica?

É possível visualizar os detalhes do volume de réplica na guia **Réplica** em **Armazenamento** > **{{site.data.keyword.filestorage_short}}**. Outra opção é selecionar o volume de réplica na página **{{site.data.keyword.filestorage_short}}** e clicar na guia **Réplica**.



## Como especificar autorizações de host antes de efetuar failover para o data center secundário?

Os hosts e volumes autorizados devem estar no mesmo data center. Não é possível ter um volume de réplica em Londres e o host em Amsterdã; ambos devem estar em Londres ou ambos devem estar em Amsterdã.

1. Clique em seu volume de origem ou destino na página **{{site.data.keyword.filestorage_short}}**.
2. Clique na guia **Réplica**.
3. Role para o quadro **Autorizar hosts** e clique em **Autorizar hosts** à direita.
4. Destaque o host que deve ser autorizado para replicações. Para selecionar múltiplos hosts, use a tecla CTRL e clique nos hosts aplicáveis.
5. Clique em **Enviar**. Se você não tiver hosts, a caixa de diálogo oferecerá a opção de comprar recursos de cálculo no mesmo data center ou será possível clicar em **Fechar**.


## Como aumentar o espaço de captura instantânea em meu data center de réplica quando aumento o espaço em meu data center primário?

Seus tamanhos de volume devem ser os mesmos para seus volumes de armazenamento primário e de réplica; um não pode ser maior que o outro. Quando você aumenta seu espaço de captura instantânea para o volume primário, o espaço de réplica é aumentado automaticamente. Esteja ciente de que aumentar o espaço de captura instantânea acionará uma atualização de replicação imediata. O aumento para ambos os volumes será mostrado como itens de linha em sua fatura e será rateado conforme necessário.

Clique [aqui](snapshots.html) para saber como aumentar seu espaço de captura instantânea.

## Como iniciar um failover de um volume para sua réplica?

No caso de um evento de falha, é possível iniciar um **Failover** para seu volume de destino ou alvo. O volume de destino torna-se ativo. A última captura instantânea replicada com êxito é ativada e o volume se torna disponível para montagem. Quaisquer dados gravados no volume de origem desde o ciclo de replicação prévio serão destruídos. Esteja ciente de que, quando um failover for iniciado, o relacionamento de replicação será invertido. Seu volume de destino é agora o volume de origem e seu antigo volume de origem se torna o destino conforme indicado pelo **REP** que segue o nome do LUN original.

Os failovers são iniciados em **Armazenamento** > **{{site.data.keyword.filestorage_short}}** no [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window}.

**Antes de continuar com esse processo, é recomendável desconectar o volume. A falha em fazer isso terminará com distorção e perda de dados.**

1. Clique em seu LUN ativo (“origem”).
2. Clique na guia Réplica e clique em **Ações** no canto superior direito.
3. Selecione **Failover**.
   Espere uma mensagem na parte superior informando que o failover está em andamento. Além disso, um ícone aparece próximo ao seu volume no **{{site.data.keyword.filestorage_short}}** indicando que uma transação ativa está ocorrendo. Passar o mouse sobre o ícone produz um diálogo indicando a transação. O ícone desaparece quando a transação está concluída. Durante o processo de failover, as ações relacionadas à configuração são somente leitura. Não é possível editar nenhum planejamento de captura instantânea ou mudar o espaço de captura instantânea e assim por diante. O evento é registrado no histórico de replicação.
4. Quando seu volume de destino está ativo, o Nome do LUN do volume de origem original é atualizado para incluir "REP" e seu Status é mostrado como Inativo.
4. Clique no link **Visualizar todo {{site.data.keyword.filestorage_short}}** no canto superior direito.
5. Clique em seu LUN ativo (anteriormente seu volume de destino). Esse volume está agora no status **Ativo**.
6. Montar e anexar seu volume de armazenamento ao host.


## Como iniciar um failback de um volume para sua réplica?

Quando o volume de origem original tiver sido reparado, a ação **failback**
permitirá iniciar um failback controlado para seu volume de origem original. Em um failback controlado,

- O volume de origem de atuação é colocado off-line;
- Uma captura instantânea é tomada;
- O ciclo de replicação é concluído;
- A captura instantânea de dados recém-tomada é ativada;
- E o volume de origem se torna ativo para montagem.

Esteja ciente de que, quando um failback é iniciado, o relacionamento de replicação é invertido novamente. Seu volume de origem é restaurado como seu volume de origem e seu volume de destino é o volume de destino novamente, conforme indicado pelo **REP** que segue o Nome do LUN.

Os failbacks são iniciados em **Armazenamento** >
**{{site.data.keyword.filestorage_short}}** no
[{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window}.

1. Clique em seu LUN do Endurance ativo ("destino").
2. Clique na guia **Réplica** e clique em **Ações** no canto superior direito.
3. Selecione **failback**.
   Espere uma mensagem na parte superior da página informando que o failover está em andamento. Além disso, um ícone aparece próximo ao seu volume indicando que uma transação ativa está ocorrendo. Passar o mouse sobre o ícone produz um diálogo indicando a transação. O ícone desaparece quando a transação está concluída. <br /> Durante o processo de failback, as ações relacionadas à configuração são somente leitura. Não é possível editar nenhum planejamento de captura instantânea, mudar o espaço de captura instantânea e assim por diante. O evento é registrado no histórico de replicação.
5. Quando seu volume de origem estiver ativo, seu volume de destino se tornará Inativo.
4. Clique em **Visualizar todo {{site.data.keyword.filestorage_short}}** no canto superior direito.
5. Clique em seu LUN ativo (origem). Esse volume está agora em um status **Ativo**.
6. Montar e anexar seu volume de armazenamento ao host. Clique [aqui](provisioning-file-storage.html) para obter instruções.


## Como ver meu histórico de replicação?

O histórico de replicação é visualizado no **Log de auditoria** na guia **Conta** em **Gerenciar**. Os volumes primário e de réplica exibem histórico de replicação idêntico, que inclui

- Tipo da replicação (failover ou failback)
- Quando ela foi iniciada
- Captura instantânea usada para a replicação
- Tamanho da replicação
- Quando ela foi concluída


## Como cancelar uma replicação existente?

O cancelamento pode ser feito imediatamente ou na data de aniversário, que faz com que o faturamento
seja finalizado. A replicação pode ser cancelada nas guias **Primário** ou **Réplica**.

1. Clique no volume na página **{{site.data.keyword.filestorage_short}}**.
2. Clique em **Ações** na guia **Primário** ou **Réplica**.
3. Selecione **Cancelar réplica**.
4. Selecione quando cancelar. **Imediatamente** ou **Data de aniversário** e clique em **Continuar**.
5. Clique na caixa de seleção **Eu reconheço que pode ocorrer perda de dados devido ao cancelamento** e clique em **Cancelar réplica**.


## Como cancelar a replicação quando o volume primário é cancelado?

Quando um volume primário é cancelado, o planejamento de replicação e o volume no data center de réplica são excluídos. As réplicas são canceladas na página **{{site.data.keyword.filestorage_short}}**.

 1. Destaque seu volume na página **{{site.data.keyword.filestorage_short}}**.
 2. Clique em **Ações** e selecione **Cancelar para o {{site.data.keyword.filestorage_short}}**.
 3. Selecione quando cancelar o volume, **Imediatamente** ou **Data de aniversário**, e clique em **Continuar**.
 4. Clique na caixa de seleção **Eu reconheço que pode ocorrer perda de dados devido ao cancelamento** e clique em **Cancelar**.
