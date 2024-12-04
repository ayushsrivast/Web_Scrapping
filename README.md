# Web_Scrapping

# Web Scraping for Electronic Bidding Information

This script scrapes information about an electronic bidding process from a government website using the `requests` and `requests_html` libraries. The script extracts specific details such as publication date, bidding date, object, and links related to the tender process.

## Requirements

Before running the script, ensure that you have the following Python libraries installed:

- `requests`
- `requests_html`

You can install the required dependencies using `pip`:

```bash
pip install requests requests_html

Script Overview
Importing Libraries
The script imports the necessary libraries for handling HTTP requests and parsing HTML:

import requests
from requests_html import HTMLSession
URL to Scrape
The target URL for the scraping operation is the electronic bidding page on the official Prefeitura de Belo Horizonte website.


url = "https://prefeitura.pbh.gov.br/saude/licitacao/pregao-eletronico-151-2020"
Handling HTTP Requests
The script uses the requests_html library to create an HTML session and send a GET request to the target URL. If any exception occurs during the request, it will be caught and printed.

try:
    session = HTMLSession()
    response = session.get(url)
except requests.exceptions.RequestException as e:
    print(e)
Extracting Data
The script extracts several pieces of information from the page using CSS selectors.

Author Information
The author's information is extracted from the element identified by the CSS selector #block-views-block-view-noticia-pbh-block-5. This information is printed as follows:

python
author = response.html.find('#block-views-block-view-noticia-pbh-block-5', first=True).text
print(author)
Publication Date, Object, and Additional Information
The script looks for the following information related to the bidding process:

Publication Date
Bidding Date
Object of the Bid
Process Number
Bank Identifier
Modality
Status
These pieces of information are collected and printed directly from the HTML response.

Tender-related Links
The script collects all the links related to the specific tender (e.g., the notice of intention, the bidding opening date, adjudication, etc.) using CSS selectors to gather the data from a table. The links are extracted and stored in a list:

python
Copy code
get_nav_links = response.html.find('tbody')
nav_links = []
 
for i in range(len(get_nav_links)):
    x = get_nav_links[i].text
    nav_links.append(x)
 
print(nav_links)
Sample Output
The output will print details like:

Author information (e.g., "atualizado em 10/03/2021 | 11:06")
Publication date ("DATA DA PUBLICAÇÃO: 02/02/2021")
Object description ("Registro de Preços pelo prazo de 12 meses, para aquisição de grampo galvanizado.")
Links related to the tender process

Example of Extracted Links

Example output for the links could be:

['Aviso de Intenção de Registro de Preços\nÍCONE DO LINK\nSEM ÍCONE\n30/10/2020\nAbertura de Licitação / Edital\nÍCONE DO LINK\nÍCONE PDF\n02/02/2021\nlink Identificador Banco do Brasil\nÍCONE DO LINK\nSEM ÍCONE\n02/02/2021\nAdjudicação e Homologação no DOM /Ata da sessão pública\nÍCONE DO LINK\nÍCONE PDF\n10/03/2021']
Customization
CSS Selectors: If the structure of the website changes, you may need to adjust the CSS selectors used for extracting data. Look for the relevant tags in the website’s HTML source and modify the response.html.find() queries accordingly.
Additional Data: You can extend this script to scrape more details related to the bidding process by adding more selectors and extracting additional data points.







