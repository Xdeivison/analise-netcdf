# Análise Climática

Este projeto realiza a análise de dados climáticos históricos e projeções futuras, calculando médias e anomalias anuais.

## Requisitos

- Python 3.7+
- xarray
- matplotlib
- pandas

## Instalação

Instale as dependências com:

```bash
pip install xarray matplotlib pandas
```

## Uso

1. Altere os caminhos dos arquivos de dados no script principal.
2. Execute o script:

```bash
python mapsv2.py
```

## Estrutura do Projeto

O projeto está organizado da seguinte forma:

- `mapsv2.py`: Script principal contendo o código para carregar dados, processá-los e gerar gráficos.
- `data/`: Diretório sugerido para armazenar os arquivos de dados NetCDF.
- `README.md`: Este arquivo, contendo instruções sobre o projeto.

## Funções Principais

- `load_data(file_path)`: Carrega dados de um arquivo NetCDF.
- `calculate_annual_mean(data, variable)`: Calcula as médias anuais de uma variável.
- `calculate_anomalies(annual_mean, climatology)`: Calcula anomalias anuais.
- `plot_data(historical_mean, rcp45_mean, rcp85_mean, historical_anomaly, rcp45_anomaly, rcp85_anomaly)`: Gera gráficos das médias e anomalias anuais.

## Exemplo de Uso

```python
# Exemplo de como usar as funções principais

# Carregar dados
historical_data = load_data('path/to/historical_data.nc')
rcp45_data = load_data('path/to/rcp45_data.nc')
rcp85_data = load_data('path/to/rcp85_data.nc')

# Calcular médias e anomalias
historical_period = historical_data.sel(time=slice('1976', '2005'))
historical_climatology = historical_period.mean(dim=['time', 'lat', 'lon'])

temperature_historical_annual_mean = calculate_annual_mean(historical_data, 'temperature')
temperature_rcp45_annual_mean = calculate_annual_mean(rcp45_data, 'temperature')
temperature_rcp85_annual_mean = calculate_annual_mean(rcp85_data, 'temperature')

temperature_historical_annual_anomaly = calculate_anomalies(temperature_historical_annual_mean, historical_climatology)
temperature_rcp45_annual_anomaly = calculate_anomalies(temperature_rcp45_annual_mean, historical_climatology)
temperature_rcp85_annual_anomaly = calculate_anomalies(temperature_rcp85_annual_mean, historical_climatology)

# Plotar dados
plot_data(temperature_historical_annual_mean, temperature_rcp45_annual_mean, temperature_rcp85_annual_mean,
          temperature_historical_annual_anomaly, temperature_rcp45_annual_anomaly, temperature_rcp85_annual_anomaly)
```
