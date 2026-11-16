# Funcionalidades e experiência de uso

[Voltar à apresentação](../README.md) · [Arquitetura](arquitetura.md)

O Forte Piano atende dois momentos complementares: preparar e organizar o acervo, e consultar o material para estudar ou ensaiar. Os fluxos centrais estão implementados e a primeira publicação foi realizada em 16/11/2026. A preparação operacional e o piloto com a orquestra ainda estão pendentes.

## Entrar e recuperar acesso

O Maestro cria o acesso da pessoa com seu e-mail e papel. O primeiro acesso parte da tela de login: a pessoa solicita um código por e-mail, valida esse código e escolhe sua senha. O fluxo de recuperação segue a mesma sequência para uma conta existente.

A validação do código usa uma sessão temporária separada. Escolher a senha não abre automaticamente o repertório: a pessoa volta ao login e entra com sua conta. O envio depende da configuração de e-mail do ambiente.

No acesso normal, o sistema verifica a sessão e a situação da conta na API. Uma identidade autenticada não libera uma conta interna bloqueada. No Android, a sessão é persistida com armazenamento seguro da plataforma.

## Encontrar uma música

O repertório permite pesquisar títulos e abrir os detalhes de uma música. A pesquisa trata diferenças de acentuação e caixa. Músicos consultam o repertório ativo; gestores também podem consultar conteúdo inativo.

Os detalhes reúnem título, categoria, observação quando preenchida e materiais organizados por tipo. O objetivo é chegar à partitura com poucos passos, mantendo os recursos de manutenção disponíveis conforme o perfil.

## Consultar partituras

Os PDFs podem ser enviados ao sistema ou associados a um acervo restrito do Google Drive. A aplicação solicita o arquivo ao backend após a verificação de acesso. As credenciais de serviço do Drive não são distribuídas no cliente.

Na Web, o leitor usa React PDF. No Android, a experiência utiliza renderização nativa e oferece:

- Navegação por páginas com toque nas laterais e deslize horizontal.
- Zoom por pinça de até 3× e arraste quando ampliado.
- Botão para ajustar novamente o documento à tela.
- Indicação da página atual e limites do documento.
- Adaptação do enquadramento após rotação.

O arquivo temporário no cache Android serve à leitura atual e é removido ao sair do leitor. Não há um acervo offline completo nesta versão.

## Ouvir materiais de apoio

O player reproduz áudios enviados ao sistema, com reprodução/pausa, seleção da faixa e controle da posição. No Android, está disponível nos detalhes e em uma área recolhível do leitor de partituras.

Recolher o player permite liberar espaço visual durante a leitura. Ao sair da tela ou colocar o aplicativo em segundo plano, a reprodução Android é pausada. Os players dos detalhes e do leitor são independentes; não há transferência automática da posição entre eles.

Links de áudio externos/YouTube e áudio do Google Drive não estão integrados ao player mobile. A existência de um link cadastrado não significa reprodução nativa suportada.

## Manter o acervo

Maestro e Arquivista podem cadastrar músicas, editar seus dados, controlar o estado ativo e administrar materiais. PDFs e áudios são vinculados à música e, quando aplicável, ao naipe correspondente.

Um fluxo comum de manutenção é:

1. Criar a música com título, categoria e observação.
2. Enviar os arquivos e associar as partes aos naipes.
3. Conferir os detalhes e a disponibilidade dos materiais.
4. Disponibilizar a música ativa para consulta dos músicos.
5. Atualizar ou remover materiais quando necessário.

As operações administrativas são protegidas na API. Categorias e naipes também possuem operações próprias no backend; isso não implica a existência de uma tela dedicada para cada operação em ambos os clientes.

## Administrar pessoas

A área de Pessoas é exclusiva do Maestro. Oferece convite, consulta paginada com busca, papel, situação da conta e vínculos com naipes. Uma pessoa pode participar de mais de um naipe.

O Maestro pode alterar papel/status de outras pessoas e gerenciar os vínculos. A própria conta é protegida contra alteração do próprio papel/status. Cada pessoa pode consultar seu perfil e editar seu próprio nome.

## Aplicar o acesso por naipe

Um músico recebe os materiais relacionados aos seus naipes e os áudios comuns sem naipe. Um PDF sem naipe não é automaticamente liberado a todos. Músicas inativas são bloqueadas para músicos também no acesso direto ao material.

Maestro e Arquivista consultam todos os materiais da música para manter o acervo. Ter o endereço de uma página não substitui a autorização do backend.

## Escopo da primeira versão

O foco é repertório, materiais, estudo e administração básica da orquestra. A versão apresentada não inclui agenda integrada, comunicados integrados, edição de anotações sobre a partitura, modo offline completo ou homologação iOS.

O ambiente foi publicado em 16/11/2026: **[site Web](https://fortepiano.duckdns.org/) e [APK Android ARM64](https://fortepiano.duckdns.org/downloads/fortepiano.apk)**. O responsável confirmou verificações iniciais da Web e a instalação/atualização do aplicativo assinado. O repertório exige uma conta autorizada; não há uma conta pública de demonstração disponibilizada neste repositório.

Ainda faltam a preparação operacional e a matriz completa de testes de acesso, leitura, áudio, permissões e uso em ensaio. Uma ocorrência de recarregamento da partitura/áudio na Web permanece aberta para investigação. Resultados do piloto serão apresentados somente depois dessa avaliação.
