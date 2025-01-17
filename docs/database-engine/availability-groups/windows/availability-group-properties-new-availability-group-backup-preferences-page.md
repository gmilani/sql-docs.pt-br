---
title: 'Propriedades do grupo de disponibilidade: Novo Grupo de Disponibilidade (página Preferências de Backup)'
description: Uma descrição das várias propriedades encontradas na página 'Preferência de Backup' do assistente 'Novo Grupo de Disponibilidade' no SQL Server Management Studio.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroupproperties.backuppreferences.f1
helpviewer_keywords:
- read-only routing
ms.assetid: 65fff22d-5963-4a8c-8b31-fe9ab247a03e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5dd782fc153829fcaa1105d37421963a8884bb0d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67991477"
---
# <a name="availability-group-properties-new-availability-group-backup-preferences-page"></a>Propriedades do grupo de disponibilidade: Novo Grupo de Disponibilidade (página Preferências de Backup)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use esta caixa de diálogo para exibir e alterar as preferências de backup do grupo de disponibilidade selecionado.  
  
 **Para exibir as propriedades do grupo de disponibilidade**  
  
-   [Exibir as propriedades do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
-   [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](~/database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="where-should-backups-occur"></a>Onde devem ocorrer os backups?  
 **Preferir Secundário**  
 Especifica que os backups devem ocorrer em uma réplica secundária, exceto quando a réplica primária for a única réplica online. Nesse caso, o backup deve ocorrer na réplica primária. Essa é a opção padrão.  
  
 **Somente Secundário**  
 Especifica que os backups nunca devem ser executados na réplica primária. Se a réplica primária for a única réplica online, o backup não deveria ocorrer.  
  
 **Primária**  
 Especifica que os backups sempre devem ocorrer na réplica primária. Essa opção será útil se você precisar de recursos de backup, como a criação de backups diferenciais, que não têm suporte quando o backup é executado em uma réplica secundária.  
  
 **Qualquer Réplica**  
 Especifica que você prefere que trabalhos de backup ignorem a função das réplicas de disponibilidade ao escolher a réplica para executar backups. Observe que os trabalhos de backup podem avaliar outros fatores, como prioridade de backup de cada réplica de disponibilidade em combinação com seu estado operacional e estado conectado.  
  
> [!IMPORTANT]  
>  Não há nenhuma imposição da configuração de preferência de backup. A interpretação dessa preferência depende da lógica, se houver, que você usa para o script em trabalhos de backup para os bancos de dados em um determinado grupo de disponibilidade. Para obter mais informações, confira [Secundárias ativas: backup em réplicas secundárias &#40;Grupos de Disponibilidade Always On&#41;](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).  
  
## <a name="replica-backup-priorities"></a>Prioridades de backup de réplica  
 Esta grade exibe a prioridade de backup atual de cada instância de servidor que hospeda uma réplica para o grupo de disponibilidade. Use essa grade para alterar a prioridade de backup de uma ou mais réplicas de disponibilidade.  
  
 **Instância do Servidor**  
 O nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda a réplica de disponibilidade.  
  
 **Prioridade de Backup (Mais Baixa = 1, Mais Alta = 100)**  
 Especifica sua prioridade para executar backups nesta réplica em relação às outras réplicas no mesmo grupo de disponibilidade. O valor é um número inteiro no intervalo de 0..100. 1 indica a prioridade mais baixa, e 100 indica a prioridade mais alta. Se **Prioridade de Backup** = 1, a réplica de disponibilidade será escolhida para execução de backups apenas se nenhuma réplica de disponibilidade de prioridade mais alta estiver disponível atualmente.  
  
 **Excluir Réplica**  
 Selecione se desejar que esta réplica de disponibilidade nunca seja escolhida para executar backups. Isso é útil, por exemplo, para uma réplica de disponibilidade remota para a qual você nunca deseja que ocorra o failover de backups.  
  
## <a name="see-also"></a>Consulte Também  
 [Secundárias ativas: backup em réplicas secundárias &#40;Grupos de Disponibilidade Always On&#41;](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  

