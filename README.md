PROYECTO-PROGRAMACON
====================

#!/usr/bin/env python
# -*- coding: utf-8 -*-

import sys
from PyQt4 import QtCore, QtGui, Qt
from PyQt4.uic import *
from datetime import *
import ConfigParser

class Myform(QtGui.QMainWindow):
    def __init__(self, parent=None):
        locale=unicode(QtCore.QLocale.system().name())
        QtGui.QWidget.__init__(self, parent)
        self.ui=loadUi("proyectomejorado.ui",self)
        self.file= "promedios.ini"
        self.date = datetime.today()
        self.config = ConfigParser.ConfigParser()
        self.show


#PRIMER TRIMESTRE
    def ok1(self):
        n1=self.ui.nota1.text()
        n2=self.ui.nota2.text()
        n3=self.ui.nota3.text()
        n4=self.ui.nota4.text()
        d1=float(self.ui.cn1.text())
        t1=float(n1)+float(n2)+float(n3)+float(n4)
        self.p1=t1/d1
        self.ui.prom1.setText(str(self.p1))


#SEGUNDO TRIMESTRE
    def ok2(self):
        n5=self.ui.nota5.text()
        n6=self.ui.nota6.text()
        n7=self.ui.nota7.text()
        n8=self.ui.nota8.text()
        d2=float(self.ui.cn2.text())
        t2=float(n5)+float(n6)+float(n7)+float(n8)
        self.p2=t2/d2
        self.ui.prom2.setText(str(self.p2))


#TERCER TRIMESTRE
    def ok3(self):
        n9=self.ui.nota9.text()
        n10=self.ui.nota10.text()
        n11=self.ui.nota11.text()
        n12=self.ui.nota12.text()
        d3=float(self.ui.cn3.text())
        t3=float(n9)+float(n10)+float(n11)+float(n12)
        self.p3=t3/d3
        self.ui.prom3.setText(str(self.p3))


#GUARDAR PROMEDIOS TRIMESTRALES
    def guardar(self):
        a=self.p1
        b=self.p2
        c=self.p3
        d=(a+b+c)/3
        self.sec2 = "Promedios :"
        cfgFile_w = open(self.file,'w')
        self.config.add_section(self.sec2)
        self.config.set(self.sec2,"1° trimestre",(a))
        self.config.set(self.sec2,"2° trimestre",(b))
        self.config.set(self.sec2,"3° trimestre",(c))
        self.config.set(self.sec2,"promedio general",(d))
        self.config.write(cfgFile_w)
        QtGui.QMessageBox.information(self, 'Mensaje de sistema', 'Se han ingresado correctamente los datos.')


    def nueva(self):
        self.modulo1=Form1()
        self.modulo1.show()
        self.close()

class Form1(QtGui.QMainWindow):
    def __init__(self, parent=None):
        locale=unicode(QtCore.QLocale.system().name())
        QtGui.QWidget.__init__(self, parent)
        self.ui=loadUi("promedio.ui",self)
        self.file= "promedios.ini"
        self.date = datetime.today()
        self.config = ConfigParser.ConfigParser()
        self.show()
        self.config.read(self.file)
        con1=self.config.get("Promedios :","1° trimestre")
        con2=self.config.get("Promedios :","2° trimestre")
        con3=self.config.get("Promedios :","3° trimestre")
        con4=self.config.get("Promedios :","promedio general")
        self.ui.prom6.setText(str(con1))
        self.ui.prom5.setText(str(con2))
        self.ui.prom4.setText(str(con3))
        self.ui.promgen.setText(str(con4))
        
    if con4>=6:
        self.ui.res.setText("Aprobo")
        print con4
    elif con4<6:
        self.ui.res.setText("Coloquio")
        print con4+"a"   
     
      
    def atras(self):
        self.modulo2=Myform()
        self.modulo2.show()
        self.close()

if __name__=="__main__":
    app=QtGui.QApplication(sys.argv)
    myapp = Myform()
    myapp.show()
    sys.exit(app.exec_())

