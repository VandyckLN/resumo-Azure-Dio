# 🚀 Criando Máquinas Virtuais no Azure: Guia Prático

Este guia é um passo a passo detalhado sobre como criar máquinas virtuais (VMs) no Microsoft Azure, pensado para ser útil para quem busca entender o processo e replicá-lo. Vamos cobrir tudo, desde a escolha da região ideal até as práticas de segurança, backup e gestão de custos.

## 📋 Índice

- [Pré-requisitos](#pré-requisitos)
- [Acessando o Portal do Azure](#acessando-o-portal-do-azure)
- [Iniciando a Criação da Máquina Virtual](#iniciando-a-criação-da-máquina-virtual)
- [Guia "Noções básicas"](#guia-noções-básicas)
- [Guia "Discos"](#guia-discos)
- [Guia "Rede"](#guia-rede)
- [Guia "Gerenciamento"](#guia-gerenciamento)
- [Guia "Monitoramento"](#guia-monitoramento)
- [Guia "Avançado"](#guia-avançado-opcional)
- [Guia "Tags"](#guia-tags-opcional-mas-recomendado)
- [Guia "Examinar + Criar"](#guia-examinar--criar)
- [Pós-Criação: Conectando-se à Sua VM](#pós-criação-conectando-se-à-sua-vm)
- [Considerações Importantes](#considerações-importantes)

## 🔍 Pré-requisitos

Para começar, você precisará de:

- Uma conta Azure ativa. Se ainda não tiver uma, pode criar uma gratuita com crédito inicial no [site do Azure](https://azure.microsoft.com/pt-br/free/).
- Permissões adequadas na sua assinatura Azure para criar e gerenciar recursos.

## 🌐 Acessando o Portal do Azure

1. Abra seu navegador e acesse o [Portal do Azure](https://portal.azure.com).
2. Faça login com suas credenciais da conta Azure.

## 🆕 Iniciando a Criação da Máquina Virtual

1. No menu de navegação esquerdo, clique em "Máquinas Virtuais".
2. Na barra superior, clique em "+ Criar" e selecione "Máquina virtual".

## 💻 Guia "Noções básicas"

Nesta seção, você configurará os detalhes essenciais da sua VM:

### Assinatura

Escolha a assinatura Azure onde a VM será criada.

### Grupo de recursos

- Um grupo de recursos é um contêiner lógico para os recursos do Azure, facilitando a organização.
- Clique em "Criar novo" e dê um nome descritivo (ex: `rg-minhavm-producao`).

### Nome da máquina virtual

Insira um nome exclusivo para sua VM (ex: `minhavm-web-01`).

### Região

- A região define a localização geográfica da sua VM (ex: Brazil South).
- Escolher uma região próxima aos seus usuários reduz a latência e melhora o desempenho.
- Considere também a disponibilidade de serviços e os preços, que podem variar.

### Opções de disponibilidade

- **Conjunto de disponibilidade**: Distribui VMs em diferentes domínios de falha e atualização dentro de um datacenter, aumentando a disponibilidade.
- **Zonas de disponibilidade**: Oferecem maior resiliência ao isolar a VM de falhas de datacenter, distribuindo-a em zonas fisicamente separadas dentro de uma região. Recomendado para cargas de trabalho críticas.
- **Conjunto de dimensionamento de máquinas virtuais**: Para gerenciar e escalar automaticamente um grande número de VMs idênticas.
- Para VMs de teste ou desenvolvimento, você pode selecionar "Nenhuma redundância de infraestrutura necessária".

### Tipo de segurança

Mantenha como "Standard" na maioria dos casos.

### Imagem

Selecione o sistema operacional da sua VM (ex: Windows Server 2022 Datacenter ou Ubuntu Server 22.04 LTS).

### Tamanho

- Escolha o tamanho da VM com base nos requisitos de CPU, memória, armazenamento e rede da sua aplicação.
- O Azure oferece diversas séries de tamanhos (ex: B-series para burst, D-series para uso geral, E-series para memória otimizada).
- Observe o custo mensal estimado exibido ao lado do tamanho.

### Conta de administrador

- **Nome de usuário**: Defina um nome de usuário para o administrador da VM.
- **Senha**: Crie e confirme uma senha forte.

### Portas de entrada públicas

- Para acesso remoto (RDP para Windows, SSH para Linux), selecione "Permitir portas selecionadas" e escolha as portas apropriadas (ex: 3389 para RDP, 22 para SSH).
- **Recomendação de segurança**: Em ambientes de produção, é altamente recomendável usar uma VPN ou Azure Bastion para acesso seguro, em vez de expor portas diretamente à internet.

Clique em "Avançar: Discos >".

## 💾 Guia "Discos"

Configure o disco do sistema operacional e, se necessário, adicione discos de dados:

### Tipo de disco do sistema operacional:

- **Premium SSD**: Alto desempenho, baixa latência. Ideal para produção.
- **Standard SSD**: Bom equilíbrio entre desempenho e custo. Adequado para desenvolvimento/teste e produção menos intensiva.
- **Standard HDD**: Menor custo, menor desempenho. Ideal para backups e dados pouco acessados.

### Chave de criptografia

Mantenha o padrão, a menos que requisitos específicos de segurança exijam uma chave gerenciada pelo cliente.

### Discos de dados

Se sua aplicação precisar de armazenamento adicional (ex: para bancos de dados, logs), clique em "Criar e anexar um novo disco" ou "Anexar um disco existente".

Clique em "Avançar: Rede >".

## 🌐 Guia "Rede"

Defina as configurações de rede da sua VM:

### Rede virtual

Crie uma nova rede virtual ou utilize uma existente. Este é o ambiente de rede isolado para sua VM.

### Sub-rede

Selecione uma sub-rede dentro da sua rede virtual para segmentação e organização.

### IP público

Crie um novo IP público se a VM precisar ser acessível pela internet. Selecione "Nenhum" se o acesso for apenas interno (ex: via VPN).

### Grupo de segurança de rede (NSG)

- Um NSG é um firewall virtual que controla o tráfego de entrada e saída.
- É fundamental configurar um NSG para controlar o acesso à sua VM. As regras de porta definidas no guia "Noções básicas" serão adicionadas aqui.

### Balanceamento de carga

Se você estiver implantando múltiplas VMs para alta disponibilidade, configure um balanceador de carga.

Clique em "Avançar: Gerenciamento >".

## ⚙️ Guia "Gerenciamento"

Nesta seção, você configurará opções de monitoramento, automação e backup:

### Diagnóstico de inicialização

Ative para auxiliar na solução de problemas de inicialização da VM.

### Identidade

Habilite uma identidade gerenciada se a VM precisar acessar outros serviços do Azure de forma segura.

### Desligamento automático

Configure para desligar a VM automaticamente em horários específicos, economizando custos para VMs de desenvolvimento ou teste.

### Backup (Azure Backup)

- O Azure Backup é um serviço robusto para proteger seus dados.
- Para configurar, selecione "Habilitar backup".
- Escolha ou crie um cofre de Serviços de Recuperação e defina uma política de backup (frequência, retenção).
- Altamente recomendado para todas as VMs de produção.

Clique em "Avançar: Monitoramento >".

## 📊 Guia "Monitoramento"

Configure o monitoramento básico para sua VM:

### Métricas de convidado do SO

Habilite para coletar métricas de desempenho do sistema operacional dentro da VM.

### Insights

Habilite o Azure Monitor Insights para obter informações detalhadas sobre o desempenho e a saúde da sua VM.

## 🔧 Guia "Avançado" (Opcional)

Esta seção permite configurar extensões, dados personalizados e outras opções mais avançadas. As configurações padrão são geralmente suficientes para a maioria dos casos.

## 🏷️ Guia "Tags" (Opcional, mas Recomendado)

As tags são pares de nome/valor usados para categorizar seus recursos.

**Exemplos**: `Ambiente: Producao`, `Projeto: WebApp`, `Responsavel: EquipeDev`.

**Benefícios**: Facilitam a organização, o gerenciamento de custos (filtrando custos por tags), a automação e a aplicação de políticas.

## 🔍 Guia "Examinar + Criar"

Revise todas as configurações da sua VM.

- O Azure executará uma validação para garantir que as configurações são válidas. Corrija quaisquer erros antes de prosseguir.
- Observe o custo estimado mensal na parte inferior.
- Após a validação, clique em "Criar".
- A implantação da VM levará alguns minutos. Você pode acompanhar o progresso no painel de notificações do Azure.

## 🔌 Pós-Criação: Conectando-se à Sua VM

Após a implantação, você pode se conectar à sua VM:

- **Para VMs Windows**: Use um cliente RDP (Conexão de Área de Trabalho Remota) e o IP público da VM.
- **Para VMs Linux**: Use um cliente SSH (ex: PuTTY ou terminal) e o IP público da VM.

## ⚠️ Considerações Importantes

### Segurança

- Sempre use senhas fortes para as contas de administrador.
- Configure Grupos de Segurança de Rede (NSG) para restringir o acesso apenas às portas e IPs necessários.
- Considere usar Azure Bastion ou VPN Gateway para acesso seguro à VM, evitando expor o RDP/SSH diretamente à internet.
- Mantenha o sistema operacional e as aplicações da VM atualizados com os patches de segurança mais recentes.
- Implemente um antivírus/antimalware dentro da VM.
- Utilize o Azure Security Center para recomendações de segurança e monitoramento contínuo.

### Disponibilidade

- Para cargas de trabalho críticas, use Zonas de Disponibilidade ou Conjuntos de Disponibilidade para garantir resiliência.
- Considere o uso de balanceadores de carga para distribuir o tráfego entre múltiplas VMs.

### Backup e Recuperação de Desastres

- Configure o Azure Backup para suas VMs, definindo políticas de backup e retenção adequadas.
- Para recuperação de desastres entre regiões, explore o Azure Site Recovery.

### Custos

- Os custos da VM são baseados no tamanho (CPU, memória, armazenamento), tipo de disco, IP público e tráfego de rede.
- Utilize o desligamento automático para VMs de desenvolvimento/teste para otimizar custos.
- Considere instâncias reservadas do Azure para cargas de trabalho de longo prazo, que podem oferecer descontos significativos.
- Monitore seus custos regularmente usando o Azure Cost Management and Billing.
- Exclua recursos que não estão mais em uso para evitar gastos desnecessários.

---

Este guia serve como um ponto de partida para a criação de VMs no Azure. Adapte as configurações às suas necessidades específicas de aplicação e negócios. Sinta-se à vontade para contribuir com sugestões ou melhorias!

## 📚 Recursos Adicionais

- [Documentação oficial do Azure Virtual Machines](https://docs.microsoft.com/pt-br/azure/virtual-machines/)
- [Melhores práticas para VMs no Azure](https://docs.microsoft.com/pt-br/azure/virtual-machines/windows/guidance-compute-single-vm)
- [Calculadora de preços do Azure](https://azure.microsoft.com/pt-br/pricing/calculator/)

## 📝 Licença

Este projeto está licenciado sob a licença MIT - veja o arquivo [LICENSE](LICENSE) para detalhes.

---

⭐ Se este guia foi útil, considere dar uma estrela no repositório! ⭐
