# project1
from PyQt5 import QtGui, QtWidgets
import sys
import random
from final import Ui_Form

class Ui(QtWidgets.QWidget):        
    def __init__(self):
        super(Ui, self).__init__()
        
        self.ui = Ui_Form()                                             # Designer Output
        self.ui.setupUi(self)
        self.ui.Status.setText("")
        self.mode = 0
        
        self.ui.LLine.textChanged.connect(self.LinesChanged)
        self.ui.ULine.textChanged.connect(self.LinesChanged)
        
        self.ui.PrintCheckBox.stateChanged.connect(self.StateChanged)
        self.ui.WriteCheckBox.stateChanged.connect(self.StateChanged)
        self.ui.GenerateButton.clicked.connect(self.Fibonacci)
        self.fail = 1
        
    def Fibonacci(self,):
        if self.fail == 1:
            return
        
        self.rand = random.randint(int(self.ui.LLine.text()), int(self.ui.ULine.text()))
        self.ui.NumberLabel.setText("The Random Number is "+str(self.rand))
        #list = 0
        for index, fibonacci_number in zip(range(self.rand), self.fib()):
            #list.append(fibonacci_number)
            print('{i:3}: {f:3}'.format(i=index, f=fibonacci_number))
        
        #self.print_text_box(list)
        #self.print_file(list)
    def print_text_box (self,list):
        ...
        
    def print_file(self,list):
        ...
        
    def fib(self,):
        a, b = 0, 1
        while True:            # First iteration:
            yield a            # yield 0 to start with and then
            a, b = b, a + b    # a will now be 1, and b will also be 1, (0 + 1)

    def LinesChanged(self,):
        self.fail = 0
        self.ui.Status.setText("")
        try:
            x=int(self.ui.LLine.text())
            x=int(self.ui.ULine.text())
        except:
            self.ui.Status.setText("ERROR:Input Must be valid Number")
            self.fail = 1
    
    def StateChanged(self,):
        if self.ui.PrintCheckBox.isChecked() and self.ui.WriteCheckBox.isChecked():
            self.mode = 1
            self.ui.Status.setText("Printing the text box and Writing the File")
        elif self.ui.PrintCheckBox.isChecked():
            self.mode = 2
            self.ui.Status.setText("Printing the text box")
        elif self.ui.WriteCheckBox.isChecked():
            self.mode = 3
            self.ui.Status.setText("Writing the File")
        else:
            self.mode = 0
            self.ui.Status.setText("")
            
            
def main():
    app = QtWidgets.QApplication([])     
    window = Ui()
    
    window.show()
    sys.exit(app.exec())
    
    
main()
  
