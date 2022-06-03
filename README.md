# projet.II-teste-
TESTE
import matplotlib.pyplot as plt
import pandas as pd
import plotly.express as px
import datetime

dados = pd.read_csv(r'dados.csv')

bs = pd.read_csv(r'dados.csv')
bs = bs.drop(["Unnamed: 0"],axis=1)
bs["DT_MEDICAO"] = pd.to_datetime(bs["DT_MEDICAO"])
bs["UMD_INS"] = pd.to_numeric(bs["UMD_INS"])
bs = bs.dropna(how='any',axis=0)
bs.info()

date_time_str_ini = '2022/01/06' #str(input('Digite a data de inicio da analise (yyyy/mm/dd)'))
date_time_obj_ini = datetime.datetime.strptime(date_time_str_ini, '%Y/%m/%d')

date_time_str_fn = '2022/06/17' #str(input('Digite a data de termino da analise (yyyy/mm/dd)'))
date_time_obj_fn = datetime.datetime.strptime(date_time_str_fn, '%Y/%m/%d')

#temperatura por tempo
fig = plt.figure(figsize=(14,7))
eixo = fig.add_axes([0,0,1,1])

eixo.plot(bs['DT_MEDICAO'], bs['TEM_INS'],color='blue')
eixo.plot(bs['DT_MEDICAO'], bs['PREV_TI'],color='red')
eixo.plot(bs['DT_MEDICAO'], bs['PREV_UI'],color='purple')
eixo.plot(bs['DT_MEDICAO'], bs['UMD_INS'],color='orange')
eixo.set_xlim(date_time_obj_ini,date_time_obj_fn)
eixo.set_title('Temperatura no momento', fontsize=25)
eixo.set_ylabel('Unidade', fontsize=20)
eixo.set_xlabel('Data', fontsize=20)
eixo.legend(['temperatura'], loc = 'lower left', fontsize=15)
eixo.grid(True)

dados.boxplot(column='TEM_INS',by='HR_MEDICAO',figsize=(16,7))

dados.hist(column="UMD_INS")
dados.UMD_INS.describe()
dados.boxplot(column="UMD_INS",by="HR_MEDICAO",figsize=(16,7))
dados.hist(column="RAD_GLO")
dados.RAD_GLO.describe()
dados.boxplot(column="RAD_GLO",by="HR_MEDICAO",figsize=(16,7))
