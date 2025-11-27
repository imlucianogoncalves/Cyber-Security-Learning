# Active Directory Basics

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

O Active Directory centraliza a administração de sistemas / grupos de computadores.

O servidor que executa o AD é conhecido como DC - Domain Controller

O core do Windows Domain é o **Active Directory Domain Service**.

Os objetos em um ADDS:

- User - ao qual tem previlégio sobre recursos como arquivos ou impressoras.

- Máquinas - não é acessada por ngm, mas sim pelo computador. 

- Security Groups - separa grupos por previlégios, permissões, etc.

Grupos comuns: 

Grupo Segurança	Descrição
Administradores de domínio	Os usuários deste grupo têm privilégios administrativos sobre todo o domínio. Por padrão, eles podem administrar qualquer computador no domínio, incluindo os DCs.
Operadores de Servidor	Os usuários deste grupo podem administrar Controladores de Domínio. Eles não podem alterar nenhuma associação a grupos administrativos.
Operadores de backup	Os usuários deste grupo podem acessar qualquer arquivo, ignorando suas permissões. Eles são usados para realizar backups de dados em computadores.
Operadores de contas	Os usuários deste grupo podem criar ou modificar outras contas no domínio.
Usuários de domínio	Inclui todas as contas de usuário existentes no domínio.
Computadores de domínio	Inclui todos os computadores existentes no domínio.
Controladores de Domínio	Inclui todos os DCs existentes no domínio.

*UOs* Organizational Unity