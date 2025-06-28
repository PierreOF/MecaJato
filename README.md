# MecaJato

MecaJato é um sistema de gerenciamento para oficinas mecânicas e lava-jatos, desenvolvido em Django. Ele permite o controle de clientes, seus veículos e os serviços prestados.

## Funcionalidades

-   **Gestão de Clientes:**
    -   Cadastro de novos clientes com informações pessoais (nome, sobrenome, e-mail, CPF).
    -   Atualização dos dados cadastrais dos clientes.
-   **Gestão de Veículos:**
    -   Cadastro de múltiplos veículos por cliente (modelo, placa, ano).
    -   Edição e exclusão de veículos.
-   **Gestão de Serviços:**
    -   Criação de ordens de serviço associadas a um cliente.
    -   Seleção de múltiplas categorias de manutenção pré-cadastradas.
    -   Adição de serviços avulsos a uma ordem de serviço existente.
    -   Geração de Ordem de Serviço (OS) em formato PDF.
    -   Listagem e acompanhamento do status dos serviços (Em manutenção / Finalizado).

## Estrutura do Projeto

O projeto é organizado em duas aplicações principais do Django:

-   `mecajato/`: Diretório principal com as configurações do projeto Django.
-   `clientes/`: Aplicação responsável por toda a lógica de CRUD de clientes e carros.
-   `servicos/`: Aplicação que gerencia as ordens de serviço, categorias de manutenção e geração de relatórios.
-   `templates/`: Contém os arquivos HTML do projeto.
    -   `static/`: Contém os arquivos estáticos (CSS, JavaScript, Imagens).
-   `manage.py`: Utilitário de linha de comando do Django.
-   `requirements.txt`: Lista de dependências Python do projeto.
-   `db.sqlite3`: Banco de dados SQLite utilizado por padrão.

## Instalação

Siga os passos abaixo para configurar o ambiente de desenvolvimento.

1.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/seu-usuario/mecajato.git](https://github.com/seu-usuario/mecajato.git)
    cd mecajato
    ```

2.  **Crie e ative um ambiente virtual:**
    ```bash
    python -m venv venv
    # Windows
    venv\Scripts\activate
    # Linux / macOS
    source venv/bin/activate
    ```

3.  **Instale as dependências:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Execute as migrações do banco de dados:**
    ```bash
    python manage.py migrate
    ```

5.  **Crie um superusuário para acessar a área administrativa:**
    ```bash
    python manage.py createsuperuser
    ```

6.  **Inicie o servidor de desenvolvimento:**
    ```bash
    python manage.py runserver
    ```

O projeto estará disponível em `http://127.0.0.1:8000`.

## Uso

-   **Gerenciar Clientes:** Acesse `http://127.0.0.1:8000/clientes/`.
-   **Adicionar e Listar Serviços:** Acesse `http://127.0.0.1:8000/servicos/novo_servico/` e `http://127.0.0.1:8000/servicos/listar_servico/`.
-   **Admin Django:** Acesse `http://127.0.0.1:8000/admin/` para gerenciar os dados diretamente, como as `CategoriaManutencao`.

## Estrutura das Tabelas

### App: `clientes`

**`Cliente`**
| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `nome` | `CharField` | Nome do cliente. |
| `sobrenome` | `CharField` | Sobrenome do cliente. |
| `email` | `EmailField` | E-mail do cliente. |
| `cpf` | `CharField` | CPF do cliente. |

**`Carro`**
| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `carro` | `CharField` | Modelo do carro. |
| `placa` | `CharField` | Placa do carro. |
| `ano` | `IntegerField` | Ano de fabricação. |
| `cliente` | `ForeignKey` | Chave estrangeira para `Cliente`.|
| `lavagens` | `IntegerField` | Contador de lavagens. |
| `consertos` | `IntegerField` | Contador de consertos. |

### App: `servicos`

**`CategoriaManutencao`**
| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `titulo` | `CharField` | Título da manutenção (ex: Troca de óleo).|
| `preco` | `DecimalField`| Preço do serviço. |

**`ServicoAdicional`**
| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `titulo` | `CharField` | Título do serviço adicional. |
| `descricao`| `TextField` | Descrição do serviço. |
| `preco` | `FloatField` | Preço do serviço adicional. |

**`Servico`**
| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `titulo` | `CharField` | Título descritivo do serviço. |
| `cliente` | `ForeignKey` | Chave estrangeira para `Cliente`. |
| `categoria_manutencao`|`ManyToManyField`| Relação com `CategoriaManutencao`.|
| `data_inicio` | `DateField` | Data de início do serviço. |
| `data_entrega`| `DateField` | Data de previsão de entrega. |
| `finalizado`| `BooleanField`| Indica se o serviço foi concluído.|
| `protocole` | `CharField` | Código de protocolo único. |
| `identificador` | `CharField` | Identificador único para a URL. |
| `servicos_adicionais`|`ManyToManyField`| Relação com `ServicoAdicional`.|

## Tecnologias Utilizadas

-   **Backend:**
    -   Python 3
    -   Django 4.1.1
-   **Frontend:**
    -   HTML5
    -   CSS3
    -   JavaScript
    -   Bootstrap 4.6
-   **Banco de Dados:**
    -   SQLite 3 (padrão)
-   **Bibliotecas Python:**
    -   `fpdf`: Para geração de relatórios em PDF.
 
créditos pelo projeto: https://www.youtube.com/@pythonando
