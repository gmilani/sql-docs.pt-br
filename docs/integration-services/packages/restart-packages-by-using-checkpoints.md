---
title: Reiniciar pacotes por meio de pontos de verificação | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- checkpoints [Integration Services]
- restarting packages
- starting packages
ms.assetid: 48f2fbb7-8964-484a-8311-5126cf594bfb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 88893b16dcb6e0529f166ab3c6e3f255110b6f71
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295780"
---
# <a name="restart-packages-by-using-checkpoints"></a>Reiniciar pacotes por meio de pontos de verificação

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pode reinicializar pacotes que falharam a partir do ponto de falha, em vez de executar novamente todo o pacote. Se um pacote estiver configurado para usar pontos de verificação, serão gravadas informações sobre a execução do pacote em um arquivo de ponto de verificação. Quando o pacote com falha é executado novamente, o arquivo do ponto de verificação é usado para reiniciar o pacote a partir do ponto de falha. Se o pacote for executado com êxito, o arquivo de ponto de verificação é excluído e recriado na próxima vez que o pacote for executado.  
  
 Usar pontos de verificação em um pacote fornece os seguintes benefícios:  
  
-   Evite repetir o download e o upload de arquivos grandes. Por exemplo, um pacote que baixa diversos arquivos grandes usando uma tarefa FTP para cada download pode ser reiniciado após o download de um único arquivo falhar e baixar apenas aquele arquivo.  
  
-   Evite repetir o carregamento de grandes quantidades de dados. Por exemplo, um pacote que realiza inserções em massa em tabelas de dimensão em um data warehouse usando uma tarefa Inserção em Massa diferente para cada dimensão pode ser reiniciado se a inserção falhar em uma tabela de dimensão e apenas essa dimensão será recarregada.  
  
-   Evite repetir a agregação de valores. Por exemplo, um pacote que computa muitas agregações, como médias e somas, usando uma tarefa de Fluxo de Dados separada para realizar cada agregação, pode ser reiniciado após computar uma falha de agregação e somente essa agregação será computada novamente.  
  
 Se um pacote for configurado para usar pontos de verificação, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] capturará o ponto de reinicialização no arquivo de ponto de verificação. O tipo de contêiner que falha e a implementação de recursos como transações afetam o ponto de reinicialização registrado no arquivo de ponto de verificação. Os valores atuais das variáveis também são capturados no arquivo de ponto de verificação. No entanto, os valores de variáveis que têm o tipo de dados **Object** não são salvos em arquivos de ponto de verificação.  
  
## <a name="defining-restart-points"></a>Definindo os pontos de reinicialização  
 O contêiner host da tarefa que encapsula uma única tarefa é a menor unidade atômica de trabalho que pode ser reiniciada. O contêiner Loop Foreach e um contêiner transacionado também são tratados como unidades atômicas de trabalho.  
  
 Se um pacote for interrompido enquanto um contêiner transacionado estiver executando, a transação será encerrada e qualquer trabalho realizado pelo contêiner será revertido. Quando o pacote for reinicializado, o contêiner que falhou será executado novamente. A conclusão de qualquer contêiner filho de contêiner transacionado não é registrada no arquivo de ponto de verificação. Portanto, quando o pacote for reinicializado, o contêiner transacionado e seus contêineres filho serão executados novamente.  
  
> [!NOTE]  
>  O uso de pontos de verificação e transações no mesmo pacote pode gerar resultados inesperados. Por exemplo, quando um pacote falha e é reiniciado em um ponto de verificação, o pacote pode repetir uma transação que já tenha sido confirmada com êxito.  
  
 Os dados do ponto de verificação não são salvos para os contêineres Loop For e Loop Foreach. Quando um pacote é reinicializado, os contêineres Loop For e Loop Foreach e seus contêineres filho são executados novamente. Se um contêiner filho no loop executar com êxito, ele não será registrado no arquivo de ponto de verificação, ao invés disso ele será executado novamente. Para obter mais informações e uma solução alternativa, consulte [Pontos de verificação do SSIS não são honrados para itens de contêiner Loop For ou Loop Foreach](https://go.microsoft.com/fwlink/?LinkId=241633).  
  
 Se o pacote for reiniciado as configurações do pacote não serão recarregadas, ao invés disso o pacote usará as informações de configuração gravadas no arquivo de ponto de verificação. Isto assegura que o pacote usará as mesmas configurações existentes no momento que falhou quando for executado novamente.  
  
 Um pacote só pode ser reinicializado no nível de fluxo de controle. Não é possível reinicializar um pacote no meio de um fluxo de dados. Para evitar executar novamente todo o fluxo de dados, o pacote deve ser projetado para incluir diversos fluxos de dados, cada um usando uma tarefa de Fluxo de Dados diferente. Deste modo o pacote pode ser reinicializado, executando apenas uma tarefa de Fluxo de Dados novamente.  
  
## <a name="configuring-a-package-to-restart"></a>Configurando um pacote para reiniciar  
 O arquivo de ponto de verificação inclui os resultados da execução de todos os contêineres concluídos, os valores atuais do sistema e variáveis definidas pelo usuário e informações de configuração do pacote. O arquivo também inclui o identificador exclusivo do pacote. Para reiniciar um pacote com êxito, o identificador do pacote no arquivo de ponto de verificação e o pacote devem corresponder; caso contrário a reinicialização falhará. Isto impede um pacote de usar um arquivo de ponto de verificação escrito por uma versão de pacote diferente. Se o pacote executar com êxito, após sua reinicialização o arquivo do ponto de verificação é excluído.  
  
 A seguinte tabela lista as propriedades de pacote definidas para implementar pontos de verificação.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|CheckpointFileName|Especifica o nome do arquivo de ponto de verificação.|  
|CheckpointUsage|Especifica se pontos de verificação são usados.|  
|SaveCheckpoints|Indica se o pacote salva os pontos de verificação. Esta propriedade deve ser definida como Verdadeiro para reinicializar um pacote a partir de um ponto de falha.|  
  
 Além disso, você deve definir a propriedade FailPackageOnFailure como **true** para todos os contêineres no pacote que deseja identificar como pontos de reinicialização.  
  
 É possível usar a propriedade ForceExecutionResult para testar o uso de pontos de verificação em um pacote. Ao definir ForceExecutionResult de uma tarefa ou contêiner como Falha, você pode imitar uma falha em tempo real. Ao executar novamente o pacote, a tarefa e os contêineres que falharam serão executados de novo.  
  
### <a name="checkpoint-usage"></a>Uso do ponto de verificação  
 A propriedade CheckpointUsage pode ser definida com os seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Never**|Especifica que o arquivo de ponto de verificação não é usado e o pacote executa a partir do início do fluxo de trabalho do pacote.|  
|**Always**|Especifica que o arquivo de ponto de verificação sempre é usado e que o pacote reinicia a partir do ponto da falha de execução anterior. Se o arquivo de ponto de verificação não for localizado, o pacote falhará.|  
|**IfExists**|Especifica que o arquivo de ponto de verificação é usado, se existir. Se o arquivo de ponto de verificação existir, o pacote reiniciará a partir do ponto da falha de execução anterior; caso contrário, será executado desde o início do fluxo de trabalho do pacote.|  
  
> [!NOTE]  
>  A opção **/CheckPointing on** de dtexec equivale a definir a propriedade **SaveCheckpoints** do pacote como **True**, e a propriedade **CheckpointUsage** como Always. Para saber mais, veja [dtexec Utility](../../integration-services/packages/dtexec-utility.md).  
  
## <a name="securing-checkpoint-files"></a>Protegendo arquivos de ponto de verificação  
 A proteção em nível de pacote não inclui proteção a arquivos de ponto de verificação; você deve proteger esses arquivos separadamente. Dados de ponto de verificação podem ser armazenados somente no sistema arquivos e você deve usar uma ACL (lista de controle de acesso) do sistema operacional para proteger o local ou a pasta onde armazena o arquivo. É importante proteger os arquivos de ponto de verificação, pois eles contém informações sobre o estado do pacote, incluindo os valores atuais de variáveis. Por exemplo, uma variável pode conter um conjunto de registros com muitas linhas de dados particulares como números de telefone. Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](../../integration-services/security/security-overview-integration-services.md#files).  

## <a name="configure-checkpoints-for-restarting-a-failed-package"></a>Configurar pontos de verificação para reinicializar um pacote com falha
  Você pode configurar os pacotes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para reiniciá-los a partir de um ponto de falha em vez de executar novamente todo o pacote, selecionando as propriedades que se aplicam aos pontos de verificação.  
  
### <a name="to-configure-a-package-to-restart"></a>Para configurar um pacote para reinicialização  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote que você deseja configurar.  
  
2.  No **Gerenciador de Soluções**, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design do fluxo de controle e clique em **Propriedades**.  
  
5.  Defina a propriedade SaveCheckpoints como **True**.  
  
6.  Digite o nome do arquivo de ponto de verificação na propriedade CheckpointFileName.  
  
7.  Defina a propriedade CheckpointUsage como um dos dois valores:  
  
    -   Selecione **Always** para reiniciar o pacote partindo sempre de um ponto de verificação.  
  
        > [!IMPORTANT]  
        >  Um erro ocorrerá se o arquivo do ponto de verificação não estiver disponível.  
  
    -   Selecione **IfExists** para reiniciar o pacote apenas se o arquivo de ponto de verificação estiver disponível.  
  
8.  Configure as tarefas e os contêineres a partir dos quais o pacote pode ser reiniciado.  
  
    -   Clique com o botão direito do mouse em uma tarefa ou contêiner e clique em **Propriedades**.  
  
    -   Defina a propriedade FailPackageOnFailure como **True** para cada tarefa e contêiner selecionado.  
    
## <a name="external-resources"></a>Recursos externos  
  
-   Artigo técnico, [Reinicialização automática de pacotes de SSIS depois de Failover ou Falha](https://go.microsoft.com/fwlink/?LinkId=200407), em social.technet.microsoft.com (a página pode estar em inglês)  
  
-   ARtigo de suporte, [Pontos de verificação do SSIS não são honrados para itens de contêiner Loop For ou Loop Foreach](https://go.microsoft.com/fwlink/?LinkId=241633), em support.microsoft.com.  
