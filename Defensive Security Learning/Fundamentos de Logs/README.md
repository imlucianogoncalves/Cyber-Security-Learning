# Fundamentos de Logs

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno SOC do TryHackMe

## IDs de Logs Relevantes

| **ID do Evento** | **Descrição** |
|------------------:|---------------|
| 4624 | Uma conta de usuário conectada com sucesso |
| 4625 | Falha no login de uma conta de usuário |
| 4634 | Uma conta de usuário desconectada com sucesso |
| 4720 | Uma conta de usuário foi criada |
| 4724 | Foi feita uma tentativa de redefinir a senha de uma conta |
| 4722 | Uma conta de usuário foi habilitada |
| 4725 | Uma conta de usuário foi desativada |
| 4726 | Uma conta de usuário foi excluída |

---

Em uma das tarefas analisei logs de uma máquina de administração de um AC - verifiquei atividades suspeitas de criação de contas e tentativa de redefinição de senha utilizando filtros a partir de IDS de ativides.

