import sys
from PyQt5.QtWidgets import QApplication, QMainWindow, QVBoxLayout, QPushButton, QWidget, QLineEdit

class Calculator(QMainWindow):
    def __init__(self):
        super().__init__()

        # Ablak beállítása
        self.setWindowTitle("Számológép")
        self.setGeometry(100, 100, 300, 400)

        # Központi widget létrehozása
        self.central_widget = QWidget(self)
        self.setCentralWidget(self.central_widget)

        # Layout beállítása
        self.layout = QVBoxLayout()
        self.central_widget.setLayout(self.layout)

        # Kijelző létrehozása
        self.display = QLineEdit(self)
        self.display.setReadOnly(True)  # Csak olvasható mező
        self.layout.addWidget(self.display)

        # Gombok létrehozása
        self.create_buttons()

    def create_buttons(self):
        """A számok és műveleti gombok létrehozása."""
        buttons = {
            '7': (0, 0), '8': (0, 1), '9': (0, 2), '/': (0, 3),
            '4': (1, 0), '5': (1, 1), '6': (1, 2), '*': (1, 3),
            '1': (2, 0), '2': (2, 1), '3': (2, 2), '-': (2, 3),
            '0': (3, 0), 'C': (3, 1), '=': (3, 2), '+': (3, 3),
        }

        # Gombok elhelyezése
        for text, pos in buttons.items():
            button = QPushButton(text)
            button.clicked.connect(lambda checked, t=text: self.on_button_click(t))
            self.layout.addWidget(button)

    def on_button_click(self, text):
        """Gombnyomás esemény kezelése."""
        if text == "C":
            # Törli a kijelző tartalmát
            self.display.setText("")
        elif text == "=":
            try:
                # Kiértékeli a kijelző tartalmát
                result = eval(self.display.text())
                self.display.setText(str(result))
            except Exception:
                self.display.setText("Error")
        else:
            # Hozzáadja a kijelző tartalmához a lenyomott gombot
            current_text = self.display.text()
            self.display.setText(current_text + text)

#alkalmazas futtatás

if __name__ == "__main__":
    app = QApplication(sys.argv)
    window = Calculator()
    window.show()
    sys.exit(app.exec_())
    
  

