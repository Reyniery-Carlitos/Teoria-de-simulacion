# Proyecto #1: Simulador datasets

**Nombre:** Carlos Reyniery Rubio Dominguez  
**Cuenta:** 20201003545  
**Catedratico:** Ing. Uayeb Caballero  
**Clase:** Teoria de simulacion  
**Fecha:** 12/07/2024  

## Estructura
- **Importar modulos**
Se importan todos los modulos necesarios para la aplicacion, para este proyecto se utilizaron los siguientes:
    1. **pandas:** Para la analisis, manipulacion y tratamiento de conjuntos de datos.
    2. **numpy:** Para la generacion y manipulacion de datos  aleatorios. 
    3. **uuid:** Para la generacion de id's unicos de 16 caracteres hexadecimales.
    4. **scipy:** Para este proyecto, concretamente el metodo truncorm el cual nos sirve para generar valores aleatorios de una funcion normal truncada.

- **Random Values Generators**
Son un conjunto de funciones que se encargan de la generacion de conjuntos de datos aleatorios, entre los cuales estan: 
    1. **generate_truncated_normal_data:** Generar una cantidad n de datos considerando la funcion normal truncada a partir de su min, max, mean y std. 
    2. **generate_category_random_values:** Generar una cantidad n de valores aleatorios de tipo categoricos.
    3. **generate_unique_random_values:** Generar una cantidad n de valores aleatorios de tipo unique (o lo que es lo mismo id's hexadecimales de 16 caracteres).
    4. **generate_date_random_values:** Generar una cantidad n de valores aleatorios de tipo fecha considerando una fecha min y max.
    5. **generate_foreign_random_values:** Generar una cantidad n de valores aleatorios de tipo foreign (o lo que es lo mismo, referencias a otro dataframe).
    6. **generate_numeric_random_values:** Generar una cantidad n de valores aleatorios de tipo numericos considerando su valor min y max; y, en otros casos, tambien considerando su mean y std (media y desviacion estandar).

- **Random Dataset Simulations Generators**
Contiene funciones que se encargan de generar datasets de valores aleatorios simulados.
    1. **get_categorical_dataset_simulated:** Se encarga de generar un conjunto de registros de cantidad n agrupados por columnas categoricas de manera aleatoria en base a su frecuencia.
    2. **get_numeric_column_simulated:** Se encarga de generar un onjunto de registros de columnas numericas en base a su resumen estadistico (min, max, mean y std) de agrupaciones de datos.

- **Helpers**
Contiene un conjunto de funciones de ayuda extra.
    1. **calc_greater:** Calcular cual es la columna con mayor cantidad de registros y devolver el valor mayor.
    2. **validate_relationships:** Valida que las columnas a las que hace referencia un dataset exitan, en caso que no devuelve un error.
    3. **extract_dependencies:** Funcion que extrae las dependencias de algun settings.
    4. **reorder_by_dependencies:** Funcion que reordena por dependencias el arreglo conf_list el cual al principio podria no estar ordenado por dependencias.
    5. **generate_df:** Funcion que genera los dataframes en base a su configuracion.

- **Main**
Funcion principal de la aplicacion.
    1. **build_dataframes:** Funcion que toma como parametro una lista de configuraciones y en base a ella genera todos los dataframes necesarios.

- **Settings**
Contiene todos los diccionarios con sus respectivas configuraciones

- **Requisito #5**
Inicio de la solucion al requisito final.

- **Analisis mejor combinacion de variables categoricas**
Realiza el analisis de columnas categoricas en base a la frecuencia de sus agrupaciones.

- **Analisis mejor combinacion de variables categoricas despues de generar los n cantidad de registros**
Realiza un analisis de las columnas categoricas en base a la frecuencia de sus agrupaciones pero despues de haber generado la n cantidad de registros aleatorios.

- **Comparacion del analisis antes y despues de generar los n cantidad de registros**
Realiza una comparacion de que tanto cambiaron las probabilidades antes y despues de haber generado los valores aleatorios en base a sus frecuencias. 

## Solucion
- **Configuraciones**
    - **Requisito #1**
        Configuracion de ejemplo #1
        ```
        d1 = {
            "ds": "dataset",
            "columns": [
                {
                    "name": "area",
                    "type": "category",
                    "values": ["TI", "FIN", "HR"]
                },
                {
                    "name": "id",
                    "type": "unique"
                }
            ],
            "random": False
        }
        ```

        Configuracion de ejemplo #2
        ```
        d1 = {
            "ds": "dataset",
            "columns": [
                {
                    "name": "area",
                    "type": "category",
                    "values": ["TI", "FIN", "HR"]
                },
                {
                    "name": "id",
                    "type": "unique"
                },
                {
                    "name": "fecha",
                    "type": "date",
                    "values": {
                        "min": "2024-01-01",
                        "max": "2024-02-28"
                    }
                }
            ],
            "random": False
        }
        ```

        Configuracion de ejemplo #3
        ```
        d1 = {
            "ds": "dataset",
            "columns": [
                {
                    "name": "area",
                    "type": "category",
                    "values": ["TI", "FIN", "HR"]
                },
                {
                    "name": "id",
                    "type": "unique"
                }
            ],
            "random": True,
            "random_rows": 1000
        }
        ```

    - **Requisito #2**
        Configuracion de ejemplo
        ```
        d2 = {
            "ds": "dataset2",
            "columns": [
                {
                    "name": "id",
                    "type": "unique"
                },
                {
                    "name": "area",
                    "type": "foreign",
                    "values": "dataset.area"
                },
                {
                    "name": "subarea",
                    "type": "category",
                    "values": ["SA1", "SA2", "SA3", "SA4"]
                }
            ],
            "random": False
        }
        ```

    - **Requisito #3**
        Configuracion de ejemplo
        ```
        d3 = {
            "ds": "dataset3",
            "columns": [
                {
                    "name": "id",
                    "type": "unique"
                }, 
                {
                    "name": "subarea",
                    "type": "foreign",
                    "values": "dataset2.id"
                },
                {
                    "name": "income",
                    "type": "numeric",
                    "values": {
                        "min": 0,
                        "max": 10000
                    }
                },
                {
                    "name": "goal",
                    "type": "numeric",
                    "values": {
                        "min": 0,
                        "max": 50000,
                        "std": 20000,
                        "mean": 25000
                    }
                }
            ],
            "random": True,
            "random_rows": 1000
        }
        ```

    - **Requisito #4**
        Configuracion de ejemplo
        ```
        d4 = {
            "ds": "dataset4",
            "columns": [
                {
                    "name": "area",
                    "type": "category",
                    "values": ["TIC", "FIN", "HR", "MKT"]
                },
                {
                    "name": "Fecha",
                    "type": "date",
                    "values": {
                        "min": "2024-01-01",
                        "max": "2024-02-28"
                    }
                },
                {
                    "name": "subarea",
                    "type": "foreign",
                    "values": "dataset3.id"
                },
                {
                    "name": "id",
                    "type": "unique"
                }
            ],
            "random": False
        }
        ```

    - **Requisito #5**
        Configuracion de ejemplo
        ```
        d5 = {
            "ds": "dataset5",
            "columns": [
                {
                    "name": "id",
                    "type": "unique"
                }, 
                {
                    "name": "area",
                    "type": "category",
                    "values": ["TIC", "FIN", "HR", "MKT"]
                },
                {
                    "name": "subarea",
                    "type": "category",
                    "values": ["SA1", "SA2", "SA3", "SA4"]
                },
                {
                    "name": "income",
                    "type": "numeric",
                    "values": {
                        "min": 0,
                        "max": 10000
                    }
                },
                {
                    "name": "goal",
                    "type": "numeric",
                    "values": {
                        "min": 0,
                        "max": 50000,
                        "std": 20000,
                        "mean": 25000
                    }
                }
            ],
            "random": True,
            "random_rows": 1000
        }
        ```
    
- **Consideraciones**
    - **Requisito #1**
        1. Crear los dataframes ✅: Esto lo realiza la funcion generate_df.
        2. Si random = False, crear los dataframes en base al valor maximo de la columna con mayor cantidad de valores ✅.
        
        ```
        def calc_greater(cols_arr):
            max_values = 0 # Inicia en cero suponiendo que no hay nada todavia al inicio
            
            for col in cols_arr:
                col_type = col['type']

                if col_type == 'foreign':
                    pass
                
                if col_type == 'date':
                    max_values = max(max_values, pd.date_range(start=col['values']['min'], end=col['values']['max']).size)

                if col_type == 'category':
                    max_values = max(max_values, len(col['values']))

            return max_values

        max_values = calc_greater(sett['columns']) if sett['random'] == False else sett['random_rows']
        ```

        3. Generar id's unicos de 16 caracteres hexadecimales para el tipo de dato unique ✅

        ```
        def generate_unique_random_values(size):
            return [uuid.uuid4().hex[:16] for _ in range(size)]
        ```
    - **Requisito #2**
        1. Valores con el tipo foreign deben tomar los valores de la columna del dataframe al que hacen referencia ✅: Esto lo realiza la funcion del inciso c.
        2. Como random = False. sigue las reglas anteriores del requisito #1 pero las columnas foreign no se toman en cuenta para el calculo del valor mayor ✅: Esto tambien lo realiza la funcion calc_greater.
        3. Retornar error en caso que no existan tanto el dataframe como la columna a la que hacen referencia ✅. 
        ```
        def validate_relationships(all_dfs, reference_df):
            # Primero valido que exista el dataframe
            df_name, df_column = reference_df.split('.')

            # Validar por nombre del dataframe
            if df_name not in all_dfs:
                raise ValueError(f'El dataframe {df_name} no existe :(')

            # Sacamos las columnas validas
            columns = list(all_dfs[df_name].columns)

            # Validamos por columna
            if df_column not in columns:
                raise ValueError(f'La columna {df_column} no existe :( en el dataframe {df_name}. Las columnas validas son: {columns}.')
        ```
        4. Los valores de la columna de tipo foreign se toman aleatoriamente de su referencia ✅.
        ```
        def generate_foreign_random_values(serie, size):
            return np.random.choice(serie.drop_duplicates(), size)  
        ```
     - **Requisito #3**
        1. Si random = True, los valores de cantidad de registros los tomara de random_rows (Obligatorio cuando random = True) ✅: Esto lo realiza la funcion calc_greater del requisito #1.
        2. Si la configuracion para tipos numericos contiene nada mas min y max  entonces utilizar una función de distribución normal para generar los valores dentro del rango especificado; sino utilizar la funcion normal truncada para la generacion de dichos datos ✅.
        ```
        def generate_truncated_normal_data(min_val, max_val, std, mean, size):
            a, b = (min_val - mean) / std, (max_val - mean) / std
            data = truncnorm(a, b, loc=mean, scale=std).rvs(size)
            data = np.round(data, 3)
            return data
        
        def generate_numeric_random_values(min, max, std, mean, size):
            if std is not None and mean is not None:
                values = generate_truncated_normal_data(min, max, std, mean, size)
            else:
                values = np.random.uniform(min, max, size)
                values = np.round(values, 3)
            return values 
        ```
    - **Requisito #4**
        1. La implementacion debera lucir de la siguiente manera ✅: 
        ```
            d1 = {} # Toda la configuración pertinente para el dataset que definas
            d2 = {} # Toda la configuración pertinente para el dataset que definas
            d3 = {} # Toda la configuración pertinente para el dataset que definas
            d4 = {} # Toda la configuración pertinente para el dataset que definas
            d5 = {} # Toda la configuración pertinente para el dataset que definas

            conf_list = [d5, d2, d4, d1, d3]
            dataframe_list = build_dataframes(conf_list)    
        ```

        Como luce: 
        ```
        d1 = {
            "ds": "dataset",
            "columns": [
                {
                    "name": "area",
                    "type": "category",
                    "values": ["TI", "FIN", "HR"]
                },
                {
                    "name": "id",
                    "type": "unique"
                },
                {
                    "name": "Fecha",
                    "type": "date",
                    "values": {
                        "min": "2024-01-01",
                        "max": "2024-02-28"
                    }
                }
            ],
            "random": False
        }

        d2 = {
            "ds": "dataset2",
            "columns": [
                {
                    "name": "id",
                    "type": "unique"
                },
                {
                    "name": "area",
                    "type": "foreign",
                    "values": "dataset.area"
                },
                {
                    "name": "subarea",
                    "type": "category",
                    "values": ["SA1", "SA2", "SA3", "SA4"]
                }
            ],
            "random": False
        }

        d3 = {
            "ds": "dataset3",
            "columns": [
                {
                    "name": "id",
                    "type": "unique"
                }, 
                {
                    "name": "subarea",
                    "type": "foreign",
                    "values": "dataset2.id"
                },
                {
                    "name": "income",
                    "type": "numeric",
                    "values": {
                        "min": 0,
                        "max": 10000
                    }
                },
                {
                    "name": "goal",
                    "type": "numeric",
                    "values": {
                        "min": 0,
                        "max": 50000,
                        "std": 20000,
                        "mean": 25000
                    }
                }
            ],
            "random": True,
            "random_rows": 1000
        }

        d4 = {
            "ds": "dataset4",
            "columns": [
                {
                    "name": "area",
                    "type": "category",
                    "values": ["TIC", "FIN", "HR", "MKT"]
                },
                {
                    "name": "Fecha",
                    "type": "date",
                    "values": {
                        "min": "2024-01-01",
                        "max": "2024-02-28"
                    }
                },
                {
                    "name": "subarea",
                    "type": "foreign",
                    "values": "dataset3.id"
                },
                {
                    "name": "id",
                    "type": "unique"
                }
            ],
            "random": False
        }

        d5 = {
            "ds": "dataset5",
            "columns": [
                {
                    "name": "id",
                    "type": "unique"
                }, 
                {
                    "name": "area",
                    "type": "category",
                    "values": ["TIC", "FIN", "HR", "MKT"]
                },
                {
                    "name": "subarea",
                    "type": "category",
                    "values": ["SA1", "SA2", "SA3", "SA4"]
                },
                {
                    "name": "income",
                    "type": "numeric",
                    "values": {
                        "min": 0,
                        "max": 10000
                    }
                },
                {
                    "name": "goal",
                    "type": "numeric",
                    "values": {
                        "min": 0,
                        "max": 50000,
                        "std": 20000,
                        "mean": 25000
                    }
                }
            ],
            "random": True,
            "random_rows": 1000
        }

        conf_list = [d3, d2, d1, d4, d5]

        dataframe_list = build_dataframes(conf_list)
        ```
        2. Se pueden definir tantas configuraciones como sean necesarias ✅.
        3. Las dependencias podrian tener mas de dos niveles, por lo que el algoritmo deberia ser capaz de construirlas sin importar su orden ✅.
        ```
        def extract_dependencies(obj):
            dependencies = []
            
            for col in obj['columns']:
                if col['type'] == 'foreign':
                    df_name = col['values'].split('.')[0]
                    dependencies.append(df_name)
            return dependencies

        def reorder_by_dependencies(arr): # Usando el algoritmo de insertion sort
            for i, value in enumerate(arr[1:], start=1):
                value_dependencies = extract_dependencies(value)
                j = i - 1

                # Validar que j no sea menor que cero y que las dependencias del valor actual recorrido esten en el valor de la izq
                while j >= 0 and any(dep in [d['ds'] for d in arr[:j+1]] for dep in value_dependencies):
                    arr[j + 1] = arr[j]
                    j -= 1
                
                # Remplazar el valor actual despues del elemento del que dependa
                arr[j + 1] = value
            return list(reversed(arr))
        ```
        4. dataframe_list deberia de mantener el orden de conf_list ✅.
        ```
        # Reordenar considerando el orden original (conf_list)
        return  [j for i in conf_list for j in df_arr if i['ds'] == j.name] # Esto se encuentra en la funcion build_dataframes
        ``` 
    - **Requisito #5**
        1. La implementacion deberia lucir de la siguiente manera ✅: 
        ```
        d1 = {} # Toda la configuración pertinente para el dataset que
        d2 = {} # Toda la configuración pertinente para el dataset que
        d3 = {} # Toda la configuración pertinente para el dataset que
        d4 = {} # Toda la configuración pertinente para el dataset que
        d5 = {} # Toda la configuración pertinente para el dataset que

        conf_list = [d5, d2, d4, d1, d3]
        dataframe_list = build_dataframes(conf_list)

        ############# Simular dataset en funcion de su distrubución ####
        
        simulation_extended = conf_list[2]
        
        ###### Section: Analizamos cual es la mejor combinacion
        ###### de variables categoricas
        ####### Tu analisis aqui
        ##### end section
        
        category_cols = [ , , , ] ### el resultado de las columnas cate
        numeric_cols = [ , , , , ]
        
        final_simulation = (
            get_categorical_dataset_simulated(
            simulation_extended
            ,category_cols
            , 100000
        ))
        
        for nc in numeric_cols:
        dfn = get_numeric_column_simulated(
            simulated
            , simulation_extended
            , category_cols
            , nc
        )
        final_simulation = pd.merge(
            final_simulation
            , dfn.loc[:,[nc]]
            , left_index=True
            , right_index=True
        )
        
        print( final_simulation )
        ```
        Como luce: 
        ```
        # La primera parte esta en el inciso a del requisito #4.
        simulation_extended = dataframe_list[4]

        category_cols = ['area', 'subarea']
        numeric_cols = ['income', 'goal']

        # Analizamos cual es la mejor combinacion de variables categoricas
        simulation_extended['n'] = 1
        grouped_combination = simulation_extended.groupby(
            category_cols,
            as_index=False
        ).agg({
            'n': 'count'
        })

        grouped_combination.columns =  category_cols + ['count']
        grouped_combination['prob'] = grouped_combination['count'] / dataframe_list[4].shape[0]
        grouped_combination.sort_values(by='count', ascending=False)
        # End section analisis de columnas categoricas


        final_simulation = get_categorical_dataset_simulated(simulation_extended,category_cols, 100000)
        for nc in numeric_cols:
            dfn = get_numeric_column_simulated(simulated, simulation_extended, category_cols, nc) 

            final_simulation = pd.merge(
                final_simulation
                , dfn.loc[:,[nc]]
                , left_index=True
                , right_index=True
            )
        
        print(final_simulation)
        ```
## Consideraciones Extra
Uso del algoritmo insertion sort para el ordenamiento del arreglo conf_list por dependencias.