
 >[!multi-column]
>
>> [!Ideas]
>>  *No que tem pensado?*
>> - [[Análise de tendências do mundo da TI]]
>
>> [!Books]
>> *Reveja algumas coisas*
>> - [[Algoritmos - Princípios da programação.pdf]]
>> 
>
>> [!Projects]
>> *Bora construir* 
>> - [[Automatização de newsletters]]
>>
>
>> [!Quests]+
>> *BOOORAAAAAAA!!!*
>> - terminar o Performance checker


> [!Weekly Review]
> Reveja suas notas modificadas nos últimos 7 dias
> ```dataview
> TABLE  durationformat(date(now) - file.mtime, "d'd'") + " ago" AS "Modified" , file.folder AS "Path", choice(reviewed = "true", "<span class='cellTrue'>true</span>", "<span class='cellFalse'>false</span>") AS "Reviewed"
> WHERE file.mtime >= (date(today) - dur(7 days))
> AND !contains(file.name, "Template")
> AND !contains(file.name, "Homepage")
> AND !contains(file.name, "Kanban")
> AND !contains(file.tags, "#toc")
> SORT file.mtime ASC
> ```

> [!performance-checker]
> Vamos ver se realmente aprendeu
> ```dataview
> TABLE file.folder AS "Path",choice(retencao = "1", "<span class='cellFirst'>Num sabo nada</span>", choice(retencao = "2", "<span class='cellSecond'>Tá ruim fih</span>", choice(retencao = "3", "<span class='cellThird'>Com defasagem</span>", choice(retencao = "4", "<span class='cellFourth'>Bom</span>", choice(retencao = "5", "<span class='cellFifth'>Dominado</span>", "<span class='cellNull'>Não definido</span>") ) ) ) ) AS "Retention"
> WHERE file.mtime >= (date(today) - dur(30 days))
> AND !contains(file.name, "Template")
> AND !contains(file.name, "Homepage")
> AND !contains(file.name, "Kanban")
> AND !contains(file.tags, "#toc")
> SORT file.mtime ASC
> ```

