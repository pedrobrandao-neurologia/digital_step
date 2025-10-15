# 🚶 O Passo Digital

> Análise de Marcha Baseada em Sensores Inerciais do Smartphone

Uma aplicação web progressiva que utiliza os sensores de movimento do smartphone para realizar análise básica de marcha humana, calculando parâmetros biomecânicos importantes sem necessidade de equipamentos especializados.

## 📋 Sobre o Projeto

O Passo Digital é uma ferramenta de demonstração tecnológica que transforma qualquer smartphone em um dispositivo básico de análise de marcha. Utilizando apenas os acelerômetros e giroscópios embutidos no aparelho, a aplicação coleta dados durante a caminhada e calcula diversos parâmetros biomecânicos relevantes.

### ⚠️ Aviso Importante

**Esta é uma ferramenta de demonstração tecnológica baseada em pesquisa e não deve ser usada para diagnóstico clínico.** Para avaliações médicas profissionais, consulte sempre um especialista qualificado.

## ✨ Funcionalidades

- **Calibração de Sensores**: Sistema de calibração para compensar bias dos sensores
- **Coleta de Dados em Tempo Real**: Captura contínua de dados do acelerômetro e giroscópio
- **Análise Automática**: Detecção de passadas e cálculo de parâmetros de marcha
- **Múltiplos Formatos de Exportação**: CSV, JSON e PDF
- **Interface Intuitiva**: Design responsivo e amigável

## 📊 Parâmetros Calculados

A aplicação calcula os seguintes parâmetros de marcha:

- **Duração da Coleta**: Tempo total de aquisição de dados
- **Número de Passadas Detectadas**: Ciclos completos de marcha identificados
- **Tempo do Ciclo**: Duração média de um ciclo completo de marcha
- **Cadência**: Número de passos por minuto
- **Fase de Apoio**: Porcentagem do ciclo em que o pé está no chão
- **Fase de Balanço**: Porcentagem do ciclo em que o pé está no ar
- **Apoio Duplo**: Porcentagem do ciclo com ambos os pés no chão
- **Comprimento do Passo**: Distância percorrida em um passo
- **Comprimento do Ciclo**: Distância percorrida em um ciclo completo
- **Velocidade da Marcha**: Velocidade média de caminhada

## 🚀 Como Usar

### Requisitos

- Navegador moderno com suporte a API DeviceMotion (Chrome, Safari, Firefox)
- Smartphone com acelerômetro e giroscópio
- Conexão HTTPS (necessária para acesso aos sensores)

### Instruções Passo a Passo

1. **Permissão de Acesso**
   - O navegador solicitará permissão para acessar os sensores de movimento
   - Aceite para continuar com a análise

2. **Posicionamento do Dispositivo**
   - Coloque o smartphone em um bolso frontal justo da calça, OU
   - Use um cinto/suporte para fixá-lo na região da cintura ou lombar
   - Certifique-se de que o dispositivo está firmemente preso

3. **Calibração**
   - Coloque o smartphone sobre uma superfície plana e estável
   - Pressione **"Calibrar Sensores"**
   - Aguarde 2 segundos sem mover o dispositivo
   - Confirme a mensagem de calibração bem-sucedida

4. **Inserir Dados do Usuário**
   - Digite um ID para identificar a pessoa testada
   - Insira a altura em metros (ex: 1.75)

5. **Coleta de Dados**
   - Pressione **"Iniciar Coleta"**
   - Caminhe em linha reta por 20-30 segundos
   - Mantenha um ritmo natural e constante

6. **Análise**
   - Pressione **"Parar e Analisar"**
   - Aguarde o processamento dos dados
   - Visualize os resultados na tabela

7. **Exportação**
   - Escolha o formato desejado: CSV (bruto ou processado), JSON ou PDF
   - Os arquivos serão baixados automaticamente

## 🛠️ Tecnologias Utilizadas

- **HTML5**: Estrutura da aplicação
- **Tailwind CSS**: Estilização responsiva
- **JavaScript (Vanilla)**: Lógica de processamento
- **DeviceMotion API**: Acesso aos sensores do dispositivo
- **jsPDF**: Geração de relatórios em PDF
- **jsPDF-AutoTable**: Formatação de tabelas em PDF

## 📱 Compatibilidade

### Navegadores Suportados

- ✅ Chrome/Edge (Android e Desktop)
- ✅ Safari (iOS 13+)
- ✅ Firefox (Android)
- ⚠️ Requer HTTPS para acesso aos sensores

### Dispositivos

- Smartphones Android (4.4+)
- iPhone/iPad (iOS 13+)
- Tablets com sensores de movimento

## 🔬 Metodologia

### Algoritmo de Detecção de Passadas

A aplicação utiliza um algoritmo de detecção de vales (valleys) no sinal de aceleração vertical filtrado para identificar os momentos de contato inicial do pé com o solo (heel strike).

### Filtragem de Dados

- **Filtro Exponencial**: Suavização do sinal com fator α = 0.2
- **Calibração**: Compensação de bias estático dos sensores

### Cálculo de Parâmetros

- **Tempo do Ciclo**: Intervalo entre heel strikes consecutivos
- **Cadência**: 120 / tempo_do_ciclo
- **Comprimento do Passo**: Modelo empírico baseado em altura, cadência e variância da aceleração
- **Velocidade**: Comprimento do ciclo / tempo do ciclo

## 📁 Estrutura de Arquivos Exportados

### CSV Bruto
```csv
timestamp,ax,ay,az,gx,gy,gz
1234567890,0.1234,-0.5678,9.8100,0.0123,-0.0456,0.0789
```

### JSON Resultados
```json
{
  "id": "Paciente01",
  "height": "1.75",
  "date": "2025-10-14T12:30:00.000Z",
  "results": {
    "Tempo do Ciclo (s)": { "value": "1.05", "typical": "1.0 - 1.2" },
    ...
  }
}
```

## 🤝 Contribuindo

Contribuições são bem-vindas! Sinta-se à vontade para:

1. Fazer fork do projeto
2. Criar uma branch para sua feature (`git checkout -b feature/NovaFuncionalidade`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova funcionalidade'`)
4. Push para a branch (`git push origin feature/NovaFuncionalidade`)
5. Abrir um Pull Request

## 📝 Licença

Este projeto está sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.

## 🔗 Referências

Este projeto é baseado em princípios de análise de marcha estabelecidos na literatura biomecânica:

- Análise instrumental da marcha
- Uso de sensores inerciais (IMU) para avaliação de movimento
- Parâmetros espaço-temporais de marcha

## 📧 Contato

Para dúvidas, sugestões ou feedback, abra uma issue no repositório.

---

**Desenvolvido com 💙 para fins educacionais e de demonstração tecnológica**
