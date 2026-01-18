# chat-neus-catala

<p><img src="static/ok0035868-neus_catala_-5-web.jpg" alt="neus" style="max-width:100px;height:auto;"></p>

Un projecte per a xat/assistència en català basat en models de llenguatge. Aquest repositori aglutina codi, recursos i configuracions per a executar un assistent conversacional local o al núvol [...] 

## Característiques

- Suport per a converses en català.
- Arquitectura pensada per a ser fàcil d'instal·lar i desplegar.
- Fitxers de configuració per a entorns de desenvolupament i producció.
- Guia de contribució i llicència permissiva (MIT).

## Estructura del repositori

La següent estructura és orientativa; adapta-la si el teu repositori té diferent organització:

- /src - codi font de l'aplicació
- /models - scripts i recursos relacionats amb el model de llenguatge (si escau)
- /configs - fitxers de configuració (ex.: .env.example, config.yaml)
- /data - dades d'entrenament o recursos lingüístics (si aplicable)
- README.md - aquest fitxer
- LICENSE - llicència del projecte

## Requisits previs

Assegura't de tenir instal·lades les eines bàsiques abans de començar:

- Git
- Python 3.8+ (o l'entorn especificat pel projecte)
- pip o entorn virtual (venv, virtualenv, conda)
- Altres dependències específiques (vegeu requirements.txt o pyproject.toml)

## Instal·lació

1. Clona el repositori:

   git clone https://github.com/germanztz/chat-neus-catala.git
   cd chat-neus-catala

2. Crea i activa un entorn virtual (opcional però recomanat):

   python -m venv .venv
   source .venv/bin/activate   # Linux / macOS
   .\.venv\Scripts\activate  # Windows

3. Instal·la les depències:

   pip install -r requirements.txt

4. Copia i modifica el fitxer d'exemple de configuració si n'hi ha (ex.: .env.example -> .env):

   cp .env.example .env
   # Editeu .env amb les vostres claus i configuracions

## Configuració

- Configureu les claus d'API o rutes als models locals segons sigui necessari en el fitxer .env o config.yaml.
- Ajusteu paràmetres com el model per defecte, el port del servidor o la memòria usada per inferència.

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