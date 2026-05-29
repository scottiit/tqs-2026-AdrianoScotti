# Relatório de Atividade Prática 10 - TQS

## Tarefa 1 — Validador de CNPJ
* **Entrega:** (https://github.com/scottiit/tqs-2026-AdrianoScotti/pull/2)

## Tarefa 2 — Validador de Telefone Celular
* **Entrega:** (https://github.com/scottiit/tqs-2026-AdrianoScotti/pull/3)

## Tarefa 3 — Quebrar o CI (e consertar)
* **Entrega:** (https://github.com/scottiit/tqs-2026-AdrianoScotti/pull/4)

## Tarefa 4 — Branch Protection
* **Entrega:** Reflexão teórica (sem print do terminal).

* **Reflexão:**
Essa proteção impede a entrada de código quebrado em produção e desastres acidentais. Ela evita que:
1. Código com erro de sintaxe ou sem testes vá direto para a `main` ignorando o pipeline de CI.
2. Alguém sobrescreva o histórico e quebre o repositório com um `push` direto acidental.

*(Nota de execução: Não incluí o print do erro forçado no terminal porque acabei ativando e caindo nesse exato bloqueio real na prática hoje mais cedo, sem querer, durante a execução das tarefas anteriores. Como já senti o impacto da trava de segurança na pele e entendi o funcionamento, foquei apenas na entrega da reflexão teórica para esta etapa.)*

## Tarefa 5 — Mutation Testing
* **Saída do `mutmut results`:**
```text
Survived 🙁 (13)

---- src/validators.py (13) ----

8, 15, 17, 19, 26-27, 29-30, 44-45, 49, 63-64
scotti@pop-os:~/tqs-2026-AdrianoScotti$ mutmut show 64
--- src/validators.py
+++ src/validators.py
@@ -51,7 +51,7 @@
     if len(apenas_digitos) != 11 or not apenas_digitos.isdigit():
         return False
     ddd = int(apenas_digitos[:2])
-    if not (11 <= ddd <= 99):
+    if not (11 <= ddd <= 100):
         return False
     return apenas_digitos[2] == "9"



## Ajustes para PR "final"
Para concluir o PR e atender ao feedback, as seguintes correçõees foram aplicadas:

- src/validators.py: Implementada a lógica matemática completa do CNPJ (tamanho, dígitos repetidos e cálculo de DV). Assinaturas padronizadas para aceitar `str | None`.
- tests/test_validators.py: Removido comentário redundante. Adicionados testes de borda para o CNPJ (string vazia, formato inválido, DV incorreto e dígitos repetidos).
- docs/validators.js: Adicionada a função `validarCnpj` espelhando a regra de negócio do backend.
- docs/index.html: Inserida a tag `<input id="telefone">` no formulário para evitar erro de null dereference.
- README.md: Removida a linha temporária de debug "TESTE".
 
