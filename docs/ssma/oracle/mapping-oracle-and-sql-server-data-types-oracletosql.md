---
title: Mapeamento de Oracle e tipos de dados do SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Type Mapping Inheritance
ms.assetid: 05da1495-63b9-47b7-86e2-6746394a2d8a
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: e5f14f79c355317f5e5d7a047b2d2c1ca71a4acb
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262963"
---
# <a name="mapping-oracle-and-sql-server-data-types-oracletosql"></a>Mapeamento de tipos de dados do Oracle e do SQL Server (OracleToSQL)
Os tipos de banco de dados Oracle variam de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de banco de dados. Quando você converte objetos de banco de dados Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos, você deve especificar como mapear tipos de dados do Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode aceitar os mapeamentos de tipo de dados padrão, ou você pode personalizar os mapeamentos conforme mostrado nas seções a seguir.  
  
## <a name="default-mappings"></a>Mapeamentos padrão  
O SSMA tem um conjunto padrão de mapeamentos de tipo de dados. Para obter a lista de mapeamentos padrão, consulte [configurações do projeto &#40;mapeamento de tipo&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md).  
  
## <a name="type-mapping-inheritance"></a>Tipo de mapeamento de herança  
Você pode personalizar mapeamentos de tipo no nível do projeto, nível de categoria de objeto (como todos os procedimentos armazenados) ou nível de objeto. As configurações são herdadas do nível mais alto, a menos que eles sejam substituídos em um nível inferior. Por exemplo, se você mapear **smallmoney** à **money** no nível do projeto, todos os objetos no projeto usará esse mapeamento, a menos que você personalize o mapeamento no nível do objeto ou categoria.  
  
Quando você exibe o **mapeamento de tipo** guia no SSMA, o plano de fundo é codificadas por cores para mostrar quais mapeamentos de tipo são herdados. O plano de fundo de um mapeamento de tipo é amarelo para qualquer mapeamento de tipo herdado e, em branco para qualquer mapeamento especificado no nível atual.  
  
## <a name="customizing-data-type-mappings"></a>Personalizando mapeamentos de tipo de dados  
O procedimento a seguir mostra como mapear tipos de dados no projeto, no banco de dados ou no nível do objeto:  
  
**Para mapear tipos de dados**  
  
1.  Para personalizar o mapeamento de tipo de dados para todo o projeto, abra o **configurações do projeto** caixa de diálogo:  
  
    1.  Sobre o **ferramentas** menu, selecione **configurações do projeto**.  
  
    2.  No painel esquerdo, selecione **mapeamento de tipo**.  
  
        O gráfico de mapeamento de tipo e os botões aparecem no painel direito.  
  
    Ou, para personalizar o tipo de dados de mapeamento no banco de dados, tabela, exibição ou nível de procedimento armazenado, selecione o banco de dados, a categoria de objeto ou o objeto no Gerenciador de metadados do Oracle:  
  
    1.  No Gerenciador de metadados do Oracle, selecione a pasta ou o objeto para personalizar.  
  
    2.  No painel direito, clique no **mapeamento de tipo** guia.  
  
2.  Para adicionar um novo mapeamento, faça o seguinte:  
  
    1.  Clique em **Adicionar** .  
  
    2.  Sob **tipo de fonte**, selecione o tipo de dados Oracle para mapear.  
  
    3.  Se o tipo requer um comprimento, especifique o comprimento mínimo de dados para o mapeamento na **de** caixa e o comprimento máximo de dados no **para** caixa.  
  
        Isso lhe permite personalizar o mapeamento de dados maiores e menores valores do mesmo tipo de dados.  
  
    4.  Sob **tipo de destino**, selecione o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.  
  
        Alguns tipos exigem um comprimento de tipo de dados de destino. Se for necessário, insira o comprimento de dados novo na **substitua** caixa.  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Para modificar um mapeamento de tipo de dados, faça o seguinte:  
  
    1.  Clique em **Editar**.  
  
    2.  Sob **tipo de fonte**, selecione o tipo de dados Oracle para mapear.  
  
    3.  Se o tipo requer um comprimento, especifique o comprimento mínimo de dados para o mapeamento na **de** caixa e o comprimento máximo de dados no **para** caixa.  
  
        Isso lhe permite personalizar o mapeamento de dados maiores e menores valores do mesmo tipo de dados.  
  
    4.  Sob **tipo de destino**, selecione o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.  
  
        Alguns tipos exigem um comprimento de tipo de dados de destino. Se for necessário, insira o comprimento de dados novo na **substitua** caixa e, em seguida, [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Para remover um mapeamento de tipo de dados personalizada, faça o seguinte:  
  
    1.  Selecione a linha na lista de mapeamento de tipo que contém o mapeamento de tipo de dados que deseja remover.  
  
    2.  Clique em **Remover**.  
  
        Você não pode remover mapeamentos herdados. No entanto, mapeamentos herdados são substituídos pelas mapeamentos personalizados em uma categoria de objeto ou um objeto específico.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa no processo de migração é para qualquer um dos [criar um relatório de avaliação](assessing-oracle-schemas-for-conversion-oracletosql.md) ou [converter objetos de banco de dados Oracle para a sintaxe do SQL Server](converting-oracle-schemas-oracletosql.md). Se você criar um relatório de avaliação, os objetos do Oracle são convertidos automaticamente durante a avaliação.  
  
## <a name="see-also"></a>Consulte também  
[Migrando do Oracle bancos de dados para o SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
