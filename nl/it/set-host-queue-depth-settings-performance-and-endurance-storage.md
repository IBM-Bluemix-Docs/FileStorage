---

copyright:
  years: 2014, 2018
lastupdated: "2018-05-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Raccomandazione per le impostazioni della profondità di coda dell'host

Consigliamo una profondità massima della coda di I/O (input/output) di applicazione e host per ogni livello prestazioni. L'impostazione host non influenza la latenza di disco e controller, solo la latenza osservata dall'host e dall'applicazione.

<table align="center">
  <caption>Profondità coda consigliata per ogni livello IOPS </caption>
        <thead>
	    <tr>
		<th>Livello prestazioni </th>
		<th>Profondità massima della coda host </th>
	    </tr>
	</thead>
	<tbody>
   	    <tr>
		<td style="text-align: center; vertical-align: middle;">0,25 IOPS per GB</td>
		<td style="text-align: center; vertical-align: middle;">8</td>
	    </tr>
	    <tr>
		<td style="text-align: center; vertical-align: middle;">2 IOPS per GB</td>
		<td style="text-align: center; vertical-align: middle;">24</td>
	    </tr>
	    <tr>
		<td style="text-align: center; vertical-align: middle;">4 IOPS per GB</td>
		<td style="text-align: center; vertical-align: middle;">56</td>
            </tr>
         </tbody>
</table>

Una profondità di coda superiore ai numeri consigliati può aumentare la latenza I/O dell'host mentre una profondità della coda al di sotto del numero consigliato può ridurre le prestazioni I/O dell'host. Poiché ciascuna applicazione è differente, sono necessarie una regolazione e un'osservazione per raggiungere le prestazioni massime dell'archiviazione. 

La profondità di coda dell'host viene di norma regolata nel driver host bus adapter o nell'hypervisor e, a volte, nell'applicazione. I valori predefiniti standard quali 32 o 64 possono causare una latenza eccessiva di host o applicazioni.

Se un host o un hypervisor stanno utilizzando più livelli Performance, usa la profondità di coda per il livello più veloce e osserva la latenza sul livello Performance più lento. Se la latenza sul livello più basso è inaccettabile, regola la profondità di coda fino ad osservare un equilibrio tra latenza e prestazioni per tutti i livelli.
