# Issue Review prompt instructions for VS Code agents
## Main Goal 1
Your main goal is to generate Issue Review markdown according to # Issue Review Example below. Especially checklist according to the example.



## Inputs
Issue description is most of the time attached as xml export of JIRA task or sometimes described by the user in previous messasges in conversation.

## Description specification
Write what route does this affect (eg. 'dynamic/nps')

## Checklist Specification
For the checklist be as detailed as possible, include minimal 3 bullet points in every category (what could break down, for testing and implementation steps)

## Output specification
Write the answer in Czech language. Output is raw markdown.




## Sub-goals (you have to meet all)
###
### Sub-Goal 1 : Thorough analysis of code
Do a thorought analysis of code to analyse what could break down.
### Sub-Goal 2
Write down a list of files that you analysed and comment everything relevant for the issue explain.
### Sub-Goal 3 : Testing
Include section of what would you test and how.


==================== Below is only issue review example ===========================================
# Issue Review Example 
## Name - Elastic -> Opensearch

## Description

**Cíl: elasticsearch je kompletně nahrazen za opensource alternativu OpenSearch a existuje nový index “speedlogger“**

### Affected routes

[route.keyword_analyzer.overview](https://collabim.atlassian.net/issues/?jql=cf%5B10065%5D%20%3D%20%22route.keyword_analyzer.overview%22)[serp_analyzer](https://collabim.atlassian.net/issues/?jql=cf%5B10065%5D%20%3D%20%22serp_analyzer%22)
    

## Checklist

• **Co by se mohlo rozbít**

• z klientského hlediska nic -> budu dělat jako komplet novou instanci(e) / dokud nepřepnu :D

• /process-add - přidávání KW

• keyword analyzer

• SERP ANALYZER

• **To test**

• běží nová Kibana, obsahuje stejné indexy jako stávající (viz. screenshot) + navíc spedlogger

•  Kibana obsahuje saved discover nginx hits

• funguje (vrací se slova) přidávání nových KW - speciálně volání Google ADS + nevznikají chyby v SENTRY

• SERP analyzer vrací data pro minimálně 3 vymyšlené domény (viz. screenshot)

• KWA v Collabim DB vrací data (viz. screenshot); nightswatch metriky fungují; Sentry (generátory z ES fungují)

• **Postup práce**

• 1: instalovat/spustit na L OpenSearch s novou Kibanou na nových portech (ideálně pomocí Ansible)

• 1: spustit na S druhou instanci v clusteru s první

• otestovat, že cluster funguje

• .5: upravit Logstash (app i tracker)

• upravit parameters (app i tracker)

• 1: naplnit uživatelská data (excellent-serp-results-clean*, serp-domains*, keyword-suggestions*, projects*?) -> na neaktivní produkci nebo Legolasovi
## Activity - Comments

### 

Dalibor Jaroš

June 13, 2024 at 2:03 PM

Edited

po poradě s kolegy na issue review jsme zjistili, že problém je výrazně menší (není třeba vůbec opensearch) a vyřešili reindexací Kibany (smazání jejich interních indexů .kibana na obou serverech clusteru) a vytvoření znovu ![grinning face with smiling eyes](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/caa27a19-fc09-4452-b2b4-a301552fd69c/32x32/1f604.png) ===>>> redukce náročnosti tasku: 6h → 2h (včetně 0,5h přemýšlení při vyplňování bodů výše)

