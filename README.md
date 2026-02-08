# 📄✏ Sensor Fault Detection Project
**Brief:** In electronics, a **wafer** (also called a slice or substrate) is a thin slice of semiconductor, such as a crystalline silicon (c-Si), used for the fabrication of integrated circuits and, in photovoltaics, to manufacture solar cells. The wafer serves as the substrate(serves as foundation for contruction of other components) for microelectronic devices built in and upon the wafer. 

It undergoes many microfabrication processes, such as doping, ion implantation, etching, thin-film deposition of various materials, and photolithographic patterning. Finally, the individual microcircuits are separated by wafer dicing and packaged as an integrated circuit.


## 💿 Installing
1. Environment setup.
```
python -m venv venv_new
```
```
.\venv_new\Scripts\Activate.ps1   # Windows PowerShell
# or
source venv_new/bin/activate      # Linux/Mac
````
2. Install Requirements and setup
```
pip install -r requirements.txt
```
3. Run Application
```
python app.py
```

The application will run on `http://localhost:5000`

## 🔧 Built with
- **Python:** 3.14.2
- **Flask:** 3.1.2
- **pandas:** 3.0.0
- **numpy:** 2.4.2
- **scikit-learn:** 1.8.0
- **xgboost:** 3.1.3
- **pymongo:** 4.16.0
- **Machine Learning:** XGBoost Classifier
- 🏦 **Industrial Use Cases**

## 📌 Key Features
- Real-time sensor fault detection
- Machine Learning model training pipeline
- REST API for predictions
- MongoDB integration for data storage
- Web interface for file upload and predictions

