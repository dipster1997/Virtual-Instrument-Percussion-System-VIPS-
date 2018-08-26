'''
Read arff file data and smoothen and denoise the graph with a Savitzky-Golay filter. and then
compare both of the graphs
'''
import matplotlib.backends.backend_pdf
pdf = matplotlib.backends.backend_pdf.PdfPages("cleaned graph.pdf")
import scipy.io
from scipy.signal import savgol_filter
import os
i=0
import numpy as np
import matplotlib.pyplot as plt
from scipy.io import arff

finalGraph=[]

'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''
PLOTTING FUNCTION
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

def plot_data(td_data):
    ax = []    ay = []    az = []    gx = []    gy = []    gz = []    at = []    gt = []
    
    # transfer arff columns into respective arrays
    for line in td_data:
        ax.append(line['ACCX'])
        ay.append(line['ACCY'])
        az.append(line['ACCZ'])
        at.append(line['ACCT'])

        gx.append(line['GYRX'])
        gy.append(line['GYRY'])
        gz.append(line['GYRZ'])
        gt.append(line['GYRT'])

    #preparing graph
    f = plt.figure(i, figsize=(80, 80))
    plt.title('Gyroscope cleaning',  fontsize=60.0)
    
    # plotting Raw data from graph
    plt.subplot(219)
    a, = plt.plot(gx,label ="Gx raw")
    b, = plt.plot(gy,label='Gy raw')
    c, = plt.plot(gz,label="Gz raw")
    plt.xlabel('Time 5ms', fontsize=50.0)
    plt.legend(handles=[a,b,c], fontsize=50.0 )
    plt.ylabel('Gyro Values m/s^2',  fontsize=50.0)

    #Filtering
    gx = savgol_filter(gx, 13, 1)
    gy = savgol_filter(gy,7,1)
    gz = savgol_filter(gz,9,1)
    
    #Plotting filtered Graph
    plt.subplot(220)
    a, = plt.plot(gx,label ='Gx after smoothening')
    b, = plt.plot(gy,label=' Gy after smoothening')
    c, = plt.plot(gz,label=' Gz after smoothening')
    
    plt.xlabel('Time 5ms', fontsize=50.0)
    plt.ylabel('Cleaned Gyro Values', fontsize=50.0)
    plt.legend(handles=[a,b,c], fontsize=50.0)

    finalGraph.append(f)
    
    
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''
OPENING ARFF FILES AND EXTRACTING THEIR DATA INTO A DATA VECTOR
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

#  create and return data vector from arff file in given path
def read_arff_file(path):
    # create the data vector
    data, meta = arff.loadarff(path)
    return data


'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''
MAIN METHOD
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''


for filename in os.listdir((os.getcwd())+"/Testing Data"):
    data = read_arff_file("Testing Data/"+filename)
    i=i+1 #new instances of graphs every time you generate
    plot_data(data)
for fig in finalGraph: ## will open an empty extra figure 
    pdf.savefig( fig )
pdf.close()
