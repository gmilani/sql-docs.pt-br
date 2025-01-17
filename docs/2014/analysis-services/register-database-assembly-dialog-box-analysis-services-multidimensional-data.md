---
title: Registre-se a caixa de diálogo de Assembly do banco de dados (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidevstudio.assembly.registerassembly.f1
ms.assetid: 0c07cc87-fc94-456f-b878-7b23e39772b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 06647219ca5768495620bb1db60cf34910844f25
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070466"
---
# <a name="register-database-assembly-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Registrar Assembly de Banco de Dados (Analysis Services – Dados Multidimensionais)
  Use a caixa de diálogo **Registrar Assembly de Servidor** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para definir as propriedades de uma referência de assembly em um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . É possível exibir a caixa de diálogo **Registrar Assembly de Servidor** clicando com o botão direito do mouse na pasta Assemblies de uma instância ou banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no **Pesquisador de Objetos** e selecionando **Novo assembly**.  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Tipo**|Seleciona o tipo de referência de assembly. Os seguintes valores estão disponíveis:<br /><br /> **Assembly .NET**: <br />                      A referência de assembly faz referência a um assembly [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework.<br /><br /> **DLL COM**: <br />                      A referência de assembly faz referência a uma biblioteca COM.<br /><br /> <br /><br /> **\*\* Observação de segurança \* \***  assemblies COM podem representar um risco de segurança. Devido a esse risco e outras considerações, os assemblies COM foram preteridos no [!INCLUDE[ssASversion10](../includes/ssasversion10-md.md)]. Talvez não haja suporte para assemblies COM em versões futuras.|  
|**Nome do arquivo**|Digite o caminho completo e o nome do arquivo do assembly .NET ou da biblioteca COM.|  
|**...**|Clique para exibir a caixa de diálogo **Abrir** e selecionar o caminho completo e o nome do arquivo do assembly .NET ou da biblioteca COM.|  
|**Nome do assembly**|Digite para definir o nome da referência de assembly.<br /><br /> Observação: A alteração desse valor não altera o nome do assembly referido pela referência de assembly, mas em vez disso, altera o nome usado o pela [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instância ou banco de dados ao fazer referência à referência de assembly.|  
|**Incluir informações de depuração**|Selecione essa opção para incluir informações sobre depurador, se disponíveis, para o assembly .NET ou biblioteca COM.|  
|**Criar Carimbo de Data/Hora**|Exibe a data e a hora de criação da referência de assembly.|  
|**Última Atualização de Esquema**|Exibe a data e a hora da última atualização dos metadados da referência de assembly.|  
|**Origem**|Exibe a origem da referência de assembly. Essa propriedade normalmente contém o caminho completo e o nome de arquivo do assembly referido pela referência de assembly.|  
|**Safe**|Selecione essa opção para usar esse conjunto de permissões para a referência de assembly. Se essa opção estiver selecionada, o assembly só terá permissão para computação interna e acesso a dados locais. O código executado por um assembly com esta opção não pode acessar recursos do sistema externo, como arquivos, rede, variáveis de ambiente ou Registro.<br /><br /> **\*\* Observação de segurança \* \***  essa opção é a configuração de permissão recomendada para assemblies que executam tarefas de gerenciamento de computação e dados sem acessar recursos externos [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Essa opção representa o conjunto de permissões mais restritivo.|  
|**Acesso externo**|Selecione essa opção para usar esse conjunto de permissões para a referência de assembly. Se essa opção estiver selecionada, o assembly só terá permissão para computação interna e acesso a dados locais. O código executado por um assembly com esse conjunto de permissões tem a habilidade de acessar recursos externos ao sistema, como arquivos, rede, variáveis de ambiente ou Registro.<br /><br /> **\*\* Observação de segurança \* \***  essa opção é recomendada para assemblies que acessam recursos fora [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Por padrão, assemblies que usam essa opção são executados usando as credenciais de segurança da conta de serviço. É possível que código dentro desse assembly personifique explicitamente o chamador [!INCLUDE[msCoName](../includes/msconame-md.md)] contexto de segurança de autenticação do Windows. Como o padrão é executar como a conta de serviço, permissão para executar assemblies com essa opção deve ser fornecida apenas a funções confiáveis para execução como a conta de serviço. Essa opção representa um conjunto de permissões menos restritivo do que **Seguro**, mas mais restritivo do que **Irrestrito**.|  
|**Unrestricted**|Selecione essa opção para usar esse conjunto de permissões para a referência de assembly. Se essa opção estiver selecionada, o assembly terá acesso irrestrito a recursos internos e externos. Código executado em um assembly com essa opção pode chamar código não gerenciado.<br /><br /> **\*\* Observação de segurança \* \***  essa opção não é recomendada a menos que o assembly exija acesso irrestrito. De uma perspectiva de segurança, essa opção é idêntica à opção **Acesso externo**. No entanto assemblies que usam a opção **Acesso externo** fornecem várias proteções de confiabilidade e robustez que não estão incluídas em assemblies que usam essa opção. A especificação dessa opção permite que o código do assembly execute operações ilegais no espaço do processo e portanto pode comprometer potencialmente a robustez e a escalabilidade do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Essa opção representa o conjunto de permissões mais restritivo e deve ser usada com cautela.|  
|**Usar nome de usuário e senha específicos**|Selecione essa opção para fazer com que o objeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] use as credenciais de segurança de uma conta de usuário especificada.|  
|**Nome de usuário**|Digite o domínio e o nome da conta de usuário a serem usados pelo objeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] selecionado. O domínio e o nome da conta de usuário usam o seguinte formato:<br /><br /> *\<Nome de domínio >* **\\**  *\<nome da conta de usuário >*<br /><br /> Observação: Essa opção estará habilitada apenas se a opção **Usar um nome e uma senha específicos** estiver selecionada.|  
|**Senha**|Digite o domínio e o nome da conta de usuário a serem usados pelo objeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] selecionado.|  
|**Usar a conta de serviço**|Selecione esta opção para fazer o objeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usar as credenciais de segurança associadas ao serviço do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que gerencia o objeto.|  
|**Usar as credenciais do usuário atual**|Selecione essa opção para fazer com que o objeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] use as credenciais de segurança do usuário atual.|  
|**Default**|Selecione essa opção para usar a conta do usuário padrão do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Selecionar essa opção é equivalente a selecionar a opção **Usar as credenciais do usuário atual** .|  
|**Descrição**|Digite para definir a descrição da referência de assembly.|  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Gerenciamento de assemblies de modelo multidimensional](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
