# O Passo Digital — Análise de Marcha com Sensores Inerciais (Web)

> **Projeto:** página HTML única que coleta **aceleração** e **giroscopia** do smartphone para estimar parâmetros espaciotemporais da marcha, com **exportação** (CSV/JSON/PDF) e **relatório** automático.  
> **Aviso:** ferramenta **demonstrativa/educacional** – **não** usar para diagnóstico clínico.

---

## ✨ Principais recursos

- **Coleta inercial** (Accelerometer/Gyroscope – Generic Sensor API) a **50 Hz**.  
- **Calibração** de bias (aceleração e giroscópio) com o dispositivo em repouso.  
- **Detecção de passos/ciclos** (vales da aceleração **z** filtrada).  
- **Estimativas espaciotemporais**:
  - Tempo de ciclo, cadência, fase de apoio/balanço, apoio duplo (estimado).
  - Comprimento do passo/ciclo e **velocidade** (estimativa baseada em altura, cadência e variância do sinal).  
- **Exportação**:
  - **Dados brutos** (CSV).
  - **Resultados** (CSV/JSON).
  - **Relatório** **PDF** com tabela formatada (jsPDF + autotable).
- **UI responsiva** com **TailwindCSS**; tipografia **Inter**.

---

## 🧠 Como funciona (resumo técnico)

1. **Permissões e sensores**  
   - Usa `Accelerometer` e `Gyroscope` (Generic Sensor API).  
   - Requer **contexto seguro (HTTPS)** e permissão do usuário.

2. **Calibração** (`Calibrar Sensores`)  
   - Coleta ~2 s em **repouso** para estimar **bias** médio de cada eixo.  
   - Ajuste de **gravidade**: `bias_z_accel = mean(z) − 9.81`.

3. **Coleta** (`Iniciar Coleta`)  
   - Amostra a **50 Hz**: `timestamp, ax, ay, az, gx, gy, gz` **corrigidos pelo bias**.

4. **Pré-processamento**  
   - **Filtro exponencial** (suavização): `α = 0.2` na componente **az**.

5. **Detecção de eventos**  
   - **Vales** em `az_filtrada` **abaixo** de `−MIN_PEAK_HEIGHT` (**1.5 m/s²**), respeitando **distância mínima** entre vales (≥ `MIN_STEP_DURATION` = **0.3 s**).

6. **Métricas**  
   - **Tempo de ciclo**: diferença entre vales consecutivos.  
   - **Cadência** ≈ `120 / tempo_ciclo_médio` (passos/min).  
   - **Apoio/Balanço (estimados)**: 60%/40% do ciclo; **apoio duplo** ≈ apoio − balanço.  
   - **Comprimento do passo** (modelo simples, **heurístico**):
     ```
     stepLength = A·height + B·cadenceHz + C·var(az) + D
     (A=0.5, B=0.05, C=0.01, D=−0.25)
     ```
     > **Observação:** coeficientes **placeholders** – não calibrados clinicamente.  
   - **Velocidade** = `strideLength / strideTime`.

7. **Apresentação e exportação**  
   - Renderiza tabela com **valor médio** e **faixas típicas** de adultos saudáveis (referenciais informativos).  
   - Exporta **CSV/JSON/PDF** com metadados (`id`, `altura`, `data`).

---

## 📦 Estrutura do projeto

Arquivo único **HTML** contendo **HTML/CSS/JS** e dependências por CDN:

- **TailwindCSS** (estilos).
- **Inter** (fonte).
- **jsPDF** e **jspdf-autotable** (PDF/relatório).

---

## 🚀 Como executar

### Opção A — GitHub Pages
1. Crie um repositório e **adicione o HTML**.
2. Em **Settings → Pages**, selecione a branch (ex.: `main`) e salve.  
3. Abra a URL publicada em **HTTPS** (necessário para acesso a sensores).

### Opção B — Local (servidor estático)
Execute um servidor simples **com HTTPS** ou, para desenvolvimento local (sem sensores), use HTTP:

```bash
# Python 3 (HTTP – pode bloquear sensores)
python -m http.server 8000
# Acesse: http://localhost:8000

