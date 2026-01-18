# chat-neus-catala

Un projecte per a xat/assistència en català basat en models de llenguatge. Aquest repositori aglutina codi, recursos i configuracions per a executar un assistent conversacional local o al núvol.

<table><tr><td style="width:200px;height:auto;">
  <img src="static/ok0035868-neus_catala_-5-web.jpg" alt="neus" >
</td>
<td>
Aquest és un treball de recerca voluntari que ha estat dissenyat per servir com a prova pilot d’un projecte més ampli. L’objectiu principal del projecte és proporcionar una interficie de xat que permeti als usuaris consultar els documents digitalitzats de la [Funcació Neus Català](https://neuscatala.cat/). 

Aquesta iniciativa busca millorar l’accessibilitat i la recerca d’aquests materials, que són d’una gran importància cultural i històrica per a la comunitat catalana. Mitjançant l’ús d’una interficie de xat, es vol facilitar la interacció amb els usuaris, permetent-los fer preguntes de manera natural i obtenir respostes basades en la consulta dels documents digitalitzats. Aquesta prova pilot pretén avaluar la viabilitat tècnica i funcional d’aquesta proposta, així com la seva utilitat per a l’ús real. 

L’interfície es dissenyarà per ser intuitiva i fàcil d’utilitzar, adaptant-se a diferents nivells de coneixement tecnològic dels usuaris. A més, es preveu que aquesta eina sigui inclusiva, permetent l’ús per a persones amb discapacitats visuals o motrius, mitjançant funcionalitats com la lectura per veu o la compatibilitat amb dispositius d’ajuda. Aquest projecte també busca contribuir a la preservació i difusió del patrimoni cultural català, fomentant la recerca acadèmica, l’ensenyament i l’interès general per la història i la cultura del nostre país. 

La prova pilot permetrà recollir feedback dels usuaris i ajustar els aspectes tècnics i de disseny segons les necessitats reals. A més, aquest treball de recerca voluntari pretén servir com a base per a futurs desenvolupaments, potenciant la col·laboració entre el sector públic, l’acadèmia i el món de la tecnologia. 

En resum, aquest projecte representa una oportunitat única per innovar en la manera com els usuaris poden accedir i explorar els documents digitalitzats de la [Funcació Neus Català](https://neuscatala.cat/), obrint camí a una nova era de consulta i interacció amb aquests materials d’interès general.
</td></tr></table>

## Característiques

Aquest projecte utilitza diverses tecnologies i llibreries per construir un sistema RAG (Retrieval-Augmented Generation) i agents basats en LLMs. A continuació es detallen les principals tecnologies trobades al codi:

- LlamaIndex (llama_index): estructura principal que facilita la creació d'índexs, ingestió de documents i la integració RAG amb eines d'emmagatzematge vectorial i LLMs.
- Ollama (llama_index.llms.ollama / Ollama, i llama_index.embeddings.ollama / OllamaEmbedding): connecta amb un servidor Ollama local (normalment a http://localhost:11434) per usar LLMs i embeddings gestionats per Ollama.
- Chroma / chromadb (chromadb.PersistentClient, ChromaVectorStore): base de vectors local/peristent usada com a magatzem per a embeddings i recerca per similaritat.
- Embeddings: s'estan utilitzant embeddings via OllamaEmbedding i també opcions de HuggingFaceEmbedding (p. ex. BAAI/bge-base-en-v1.5) o noms com qwen3-embedding, qllama/bge-small-en-v1.5:f16, jinaai/jina-embeddings-v2-base-es, nomic-embed-text.
- LLMs (manca d'una única font): exemples referenciats al codi inclouen qwen2.5 (p.ex. qwen2.5:7b-instruct, qwen2.5:32b-instruct), qwen3 (qwen3 / qwen3-embedding), llama3 (llama3.1 / llama3.2), deepseek-r1 i altres. Aquests models s'utilitzen a través d'Ollama o com a embeddings segons la configuració.
- Agent workflows i RAG: el codi fa servir AgentWorkflow, ReActAgent i eines de LlamaIndex per crear agents que combinen funcions, càlculs i recerca de documents (p. ex. QueryEngineTool, search_documents). Això permet fer preguntes naturals i recuperar context des d'un índex vectorial per a respostes més informades.
- Processament de documents: SimpleDirectoryReader, IngestionPipeline, SentenceSplitter i components personalitzats (p. ex. TextCleaner) per netejar PDFs i text (PyPDF2, regex), dividir en nodes i emmagatzemar fragments.
- Llibreries Python auxiliars: pandas, PyPDF2, python-dotenv (load_dotenv), nest_asyncio, asyncio, glob, json, re.
- Transformacions i avaluació: TransformComponent, FaithfulnessEvaluator, PromptTemplate i altres components de LlamaIndex utilitzats per preparar prompts i avaluar respostes.

Aquestes tecnologies treballen conjuntament per implementar un flux RAG on:
1) Documents es processen i es converteixen en embeddings.
2) Els embeddings s'emmagatzemen en Chroma (chromadb) per a recerques similars.
3) Quan s'activa una consulta, es recuperen fragments rellevants i es passa el context al LLM (via Ollama) per generar la resposta final.

## Estructura del repositori

La següent estructura és orientativa; adapta-la si el teu repositori té diferent organització:

- /src - codi font de l'aplicació
- /models - scripts i recursos relacionats amb el model de llenguatge (si escau)
- /configs - fitxers de configuració (ex.: .env.example, config.yaml)
- /data - dades d'entrenament o recursos lingüístics
- /static - recursos estàtics (imatges)
- README.md - aquest fitxer
- LICENSE - llicència del projecte

## Requisits previs

Assegura't de tenir instal·lades les eines bàsiques abans de començar:

- Git
- Python 3.8+ (o l'entorn especificat pel projecte)
- pip o entorn virtual (venv, virtualenv, conda)
- Docker (opcional, si prefereixes executar components en contenidors)
- Ollama (per usar models locals) — veure instal·lació més avall

## Instal·lació

1. Clona el repositori:

   git clone https://github.com/germanztz/chat-neus-catala.git
   cd chat-neus-catala

2. Crea i activa un entorn virtual (recomanat):

   python -m venv .venv
   source .venv/bin/activate   # Linux / macOS
   .\.venv\Scripts\activate  # Windows

3. Instal·la les dependències Python (exemple):

   pip install -r requirements.txt

Si no tens requirements.txt, pots instal·lar les principals llibreries utilitzades al repositori amb:

   pip install -U llama_index llama_index.llms.ollama llama_index.embeddings.ollama \
       llama_index.vector_stores.chroma llama-index-callbacks-arize-phoenix \
       llama_index.embeddings.huggingface PyPDF2 transformers torch sentence-transformers pandas python-dotenv chromadb nest_asyncio

Nota: la instal·lació de transformers/torch pot requerir versions específiques segons la teva GPU/CPU i potser instal·lar paquets GPU (CUDA) si vols inferència local ràpida.

4. Instal·lació d'Ollama i models (resum)

- Instal·lar Ollama:
  - macOS (Homebrew):
    brew install ollama
  - Linux (script d'instal·lació oficial):
    curl -sSL https://ollama.com/install.sh | sh
  - Windows: segueix la guia oficial d'Ollama (o utilitza WSL)

  Per a la informació més actualitzada, visita: https://ollama.com/docs

- Iniciar el servei Ollama (daemon/local server):
  Un cop instal·lat, apunta el codi a l'endpoint local d'Ollama que el projecte espera (per defecte): http://localhost:11434
  Consulta la documentació d'Ollama per saber com executar el servei en segon pla. Algunes versions proporcionen un servei que s'executa automàticament en instal·lar o una comanda tipus `ollama daemon`.

- Descarregar/pullar models a Ollama:
  Exemple de com obtenir alguns models mencionats al codi (ajusta noms segons disponibilitat i permisos):

    ollama pull qwen2.5:7b-instruct
    ollama pull qwen2.5:32b-instruct
    ollama pull qwen3
    ollama pull qwen3-embedding
    ollama pull llama3.2:latest
    ollama pull deepseek-r1:latest
    ollama pull qllama/bge-small-en-v1.5:f16

  Tingues en compte que alguns models poden requerir llicències o no estar disponibles públicament a través d'Ollama. Consulta la llista de models d'Ollama (`ollama list` o la documentació) per conèixer els noms exactes i la disponibilitat.

5. Configura variables d'entorn

Copia i edita el fitxer d'exemple de configuració si n'hi ha (.env.example -> .env) i afegeix les rutes/ajustos necessaris (per exemple, DATA_PATH, endpoint d'Ollama si no és el per defecte, etc.).

6. Crear índexs i executar

- Omple el directori data/ amb els documents que vulguis indexar (PDFs, textos, etc.).
- Executa els scripts d'ingestió o l'aplicació principal, per exemple:

  python neus-catala-model.py
  o l'script/entrypoint que tinguis al projecte

Això crearà (o reutilitzarà) la base de dades Chroma persistent definida a data/neus_catala.db i et permetrà fer consultes RAG a través de LlamaIndex + Ollama.

## Ús

Els passos concrets per iniciar l'aplicació poden variar segons la implementació. Exemple general:

- Inicieu el servidor:

  python -m src.app

- Obriu el navegador a http://localhost:8000 o el port configurat i comenceu a xatejar en català.

(Adapteu aquestes instruccions als scripts reals del vostre projecte, per exemple: `uvicorn src.main:app --reload` o `docker compose up`.)

## Desplegament

Opcions comunes de desplegament:

- Docker / Docker Compose
- Serveis en el núvol (AWS, GCP, Azure)
- Plataformes de PaaS (Heroku, Render, Railway)

Afegeix i documenta els fitxers de Docker si vols suportar desplegament containeritzat.

## Contribuir

Gràcies per voler contribuir! Algunes bones pràctiques:

1. Fork i crea una branca per la teva millora: `git checkout -b feature/nou-element`
2. Fes commits petits i descriptius.
3. Obre una pull request amb una descripció clara del canvi.
4. Afegeix proves i documentació si cal.

Segueix l'estil de codi existent i inclou proves unitàries en la mesura del possible.

## Reportar errors i sol·licitud de noves funcionalitats

Obre un issue a GitHub amb el títol i la descripció detallada. Inclou passos per reproduir l'error i l'entorn (OS, versions, configuracions).

## Internacionalització

Aquest projecte posa especial atenció al català. Si afegeixes suport per a altres variants (valencià, balear) o idiomes, documenta com canviar la llengua per defecte.

## Privadesa i dades

Si el projecte processa dades d'usuaris, afegeix una secció sobre com es gestionen i emmagatzemen aquestes dades, compliment de regulacions (p. ex. RGPD) i recomanacions per a anonimització.

## Llicència

Aquest projecte es distribueix sota la llicència MIT. Vegeu el fitxer LICENSE per al text complet.

## Agraïments

Gràcies a tothom que contribueix i col·labora en fer un assistent en català millor i més accessible.

---

Per qualsevol dubte o consulta, contacta amb: germanztz (https://github.com/germanztz)
