 ## Questão 1
 
O stub (cliente) e o skeleton (servidor) garantem a transparência de localização ao isolar a lógica de rede. O stub serializa os parâmetros (ex: JSON ou binário) e gerencia o envio via socket; o skeleton recebe, desserializa e despacha a execução para a função correta via dispatch table. Sem eles, o desenvolvedor teria que implementar manualmente o marshalling e o controle de fluxo em cada chamada, aumentando a complexidade e o acoplamento.
 
## Questão 2
 
A diferença reside na abstração: o RPC foca em verbos (invocação de procedimentos), enquanto o REST foca em substantivos (manipulação de recursos). No Lab, o RPC chamava calcular("soma") (ação), enquanto o REST interagia com /produtos via verbos HTTP (estado). O RPC sobre HTTP frequentemente ignora a interface uniforme, tratando o protocolo apenas como túnel, enquanto o REST utiliza o ecossistema HTTP (cache, status codes) de forma nativa.
 
## Questão 3
 
No gRPC/Protobuf, a evolução é robusta e retrocompatível: novos campos recebem números de identificação únicos, permitindo que clientes antigos ignorem dados desconhecidos sem quebrar. Já no REST/JSON, a evolução é baseada em convenção; embora flexível para adicionar campos, a ausência de um schema rígido e de verificação estática aumenta o risco de erros de tipagem em tempo de execução caso o contrato mude sem aviso.
 
## Questão 4
 
APIs Externas (Parceiros): Recomenda-se REST. Sua ubiquidade, facilidade de teste via browser e suporte universal a JSON eliminam a barreira de entrada (sem necessidade de compilar arquivos .proto).

Comunicação Interna (Microsserviços): Recomenda-se gRPC. O contrato forte e a serialização binária otimizam a performance e garantem segurança de tipos entre equipes, aproveitando a infraestrutura controlada para padronizar a geração de código.

 
## Questão 5
 
Embora o RPC simplifique a codificação ao fazer uma chamada remota parecer local, essa "transparência excessiva" pode ser uma armadilha. O desenvolvedor pode ignorar falhas parciais, latência de rede e o custo de serialização. É vital manter a consciência da fronteira: chamadas distribuídas exigem estratégias de timeout, retries e tratamento de erros (como RpcError), evitando que a facilidade de uso resulte em sistemas frágeis ou lentos.
