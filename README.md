# Passo a passo para criação de uma VM no Azure

Este documento fornece um passo a passo direto e simplificado para a criação de uma Máquina Virtual (VM) através do portal Microsoft Azure, focando nos procedimentos essenciais para uma configuração inicial funcional.

## 1. Acesso ao Portal e Início do Processo

O primeiro passo é acessar sua conta no portal do Azure.

    Acesse o Portal: Abra seu navegador e vá para https://portal.azure.com.
    Autenticação: Realize o login com as credenciais associadas à sua assinatura do Azure.
    Localize o Serviço: Na barra de busca principal, digite "Máquinas Virtuais" e selecione o serviço correspondente.
    Inicie a Criação: Na página de "Máquinas Virtuais", clique no botão "+ Criar" e, no menu suspenso, escolha "Máquina virtual".

## 2. Configurações Fundamentais (Aba "Básico")

Esta seção é crucial, pois define as características principais da sua máquina virtual.

    Assinatura e Grupo de Recursos:
        Assinatura: Selecione a assinatura do Azure que será utilizada para o faturamento dos recursos.
        Grupo de Recursos: Este é um contêiner lógico para agrupar os recursos da sua solução. Recomenda-se criar um novo para melhor organização (ex: RG-ServidorPrincipal).

    Detalhes da Instância:
        Nome da máquina virtual: Atribua um nome único e claro (ex: VM-WebServer01).
        Região: Escolha o datacenter onde a VM será provisionada. Para menor latência, selecione uma localização geograficamente próxima aos seus usuários (ex: (South America) Brazil South).
        Imagem: Selecione o sistema operacional (SO) base. Opções comuns incluem:
            Ubuntu Server LTS: Versões estáveis e com suporte de longo prazo do Linux.
            Windows Server Datacenter: Sistema operacional de servidor da Microsoft.
        Tamanho: Defina a configuração de hardware (CPU e Memória RAM). Para testes iniciais, a série B (econômica) ou D (uso geral) são pontos de partida adequados.

    Conta de Administrador:
        Tipo de autenticação:
            Senha: Método simples, ideal para testes rápidos. Requer a definição de um nome de usuário e uma senha forte.
            Chave pública SSH (Linux): Método mais seguro para ambientes de produção. Requer que você forneça a parte pública de um par de chaves SSH.
        Credenciais: Preencha o nome de usuário e a senha (ou chave) conforme a escolha acima.

## 3. Configuração de Rede (Aba "Rede")

Para uma configuração inicial, as opções padrão do Azure são geralmente suficientes e seguras.

    Rede Virtual (VNet): O Azure criará automaticamente uma nova rede virtual para isolar sua VM.
    Sub-rede: Dentro da VNet, uma sub-rede padrão será configurada.
    IP Público: Um endereço de IP público será criado e associado à VM, permitindo o acesso a ela pela internet.
    Grupo de Segurança de Rede (NSG): Funciona como um firewall virtual. É fundamental liberar as portas corretas para acesso:
        SSH (porta 22): Para acesso ao terminal em VMs Linux.
        RDP (porta 3389): Para acesso à área de trabalho remota em VMs Windows.

## 4. Revisão e Criação (Aba "Revisar + criar")

A etapa final consiste em verificar as configurações e iniciar a implantação.

    Validação: O Azure analisará suas configurações. Uma mensagem de "Validação aprovada" indicará que tudo está correto.
    Revisão: Um resumo de todos os recursos a serem criados será exibido. Verifique se as escolhas estão de acordo com o planejado.
    Criação: Clique em "Criar" para iniciar o processo de provisionamento.
        Atenção (para SSH): Caso tenha optado por autenticação via chave SSH, o portal solicitará o download da chave privada (.pem). É imperativo que você guarde este arquivo em um local seguro, pois ele não poderá ser recuperado posteriormente.

O processo de implantação levará alguns minutos. O andamento pode ser acompanhado através do ícone de notificações (sino) no canto superior direito do portal.

## 5. Conexão com a Máquina Virtual

Uma vez que a implantação esteja concluída, acesse sua VM.

    Navegue até a página de recursos da sua nova máquina virtual.
    Clique no botão "Conectar" no menu superior.

<!-- end list -->

    Para Windows (via RDP): O portal fornecerá um arquivo de conexão .rdp. Faça o download, execute-o e utilize o usuário e a senha definidos na etapa 2 para se conectar.
    Para Linux (via SSH): O portal exibirá o comando de conexão necessário. Copie o comando, que terá o formato ssh -i <chave_privada.pem> usuario@<ip_publico>, e execute-o em seu terminal ou cliente SSH.
