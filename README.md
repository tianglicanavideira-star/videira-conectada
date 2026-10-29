# Videira Conecta — starter de aplicativo

Aplicativo web instalável (PWA) para a Igreja Anglicana Videira, criado com React + Vite + TypeScript e Supabase.

## O que já está no projeto

- Interface responsiva para computador e celular.
- Navegação: Início, Minhas escalas, Agenda, Ministérios, Bíblia offline, Parceiros, Galeria, Notícias e Administração.
- Tela de login/cadastro integrada ao Supabase quando as variáveis de ambiente são configuradas.
- Consultas reais para eventos, escalas do usuário, notícias publicadas e parceiros aprovados.
- Formulários iniciais de criação de evento e rascunho de notícia.
- Schema SQL com tabelas, trigger de perfil e políticas RLS iniciais.
- Manifest e service worker de base para instalação/cache.
- Dados demonstrativos para pré-visualizar a interface sem conexão ao banco.

## Requisitos

- Node.js 20 ou superior
- Conta Supabase
- Conta Vercel (para hospedagem gratuita, sujeita aos termos e limites atuais)

## Executar localmente

1. Instale Node.js.
2. Extraia o ZIP e abra a pasta `videira-conecta` no terminal.
3. Execute `npm install`.
4. Copie `.env.example` para `.env` e preencha as chaves públicas do seu projeto Supabase.
5. Execute `npm run dev` e abra o endereço local indicado pelo Vite.
6. Para validar a versão de produção, execute `npm run build`.

Sem as variáveis Supabase, o projeto abre em modo de demonstração; login e gravação real não estarão ativos.

## Configurar o Supabase

1. Crie um projeto no painel do Supabase.
2. No SQL Editor, execute o conteúdo de `supabase/schema.sql`.
3. Em Project Settings / API, copie a Project URL e a chave pública `anon`/publishable para `.env`.
4. Cadastre uma conta de administrador pelo formulário de login/cadastro.
5. No painel do Supabase, abra Table Editor > profiles e altere o `role` desse usuário para `admin`.
6. Em Authentication, configure confirmação de e-mail e URLs de redirecionamento para desenvolvimento e produção.
7. Teste com contas separadas: admin, líder e membro. Revise todas as políticas antes de colocar dados reais.

**Segurança:** nunca coloque a `service_role` key no frontend. O app_role `leader` existe no schema, mas a interface de administração ainda é inicial e precisa de uma tela de gestão de ministérios/atribuições antes do uso operacional completo. A promoção de administradores é manual no banco por segurança.

## Publicar na Vercel

1. Coloque o código em um repositório Git privado/público sob controle da igreja.
2. Na Vercel, importe o repositório.
3. Defina build command `npm run build` e output directory `dist`.
4. Configure `VITE_SUPABASE_URL` e `VITE_SUPABASE_ANON_KEY` em Environment Variables.
5. Publique e teste o endereço `*.vercel.app`.
6. Atualize as URLs autorizadas do Supabase para o endereço publicado.

A disponibilidade de subdomínio e plano gratuito depende das condições atuais do fornecedor. Não é necessário comprar domínio próprio para usar o subdomínio da Vercel.

## Pontos que ainda precisam ser concluídos antes de produção

Este é um starter funcional, não uma implantação já publicada. Para considerar o sistema pronto para uso real, ainda é necessário:
- Criar o projeto Supabase e fornecer suas chaves públicas por variáveis de ambiente.
- Fazer deploy a partir de uma conta autorizada.
- Testar e revisar RLS e fluxos de acesso.
- Criar telas completas para administrar membros, ministérios e escalas.
- Completar upload e moderação de fotos.
- Definir a tradução bíblica integral e confirmar a licença para uso offline.
- Configurar notificações push (exigem configuração adicional).
- Implementar consentimento e governança de dados de acordo com a LGPD, inclusive regras para fotos de menores.
- Adicionar testes automatizados, monitoramento e backups.

## Observação sobre a Bíblia offline

A tela contém somente pequenos trechos de demonstração, não uma Bíblia completa. Não distribua uma tradução sem confirmar sua licença. O service worker fornece apenas cache básico do shell da aplicação; o conteúdo bíblico completo offline e sua busca precisam ser implementados depois que uma tradução licenciada for escolhida.
