import streamlit as st
import numpy as np
from fractions import Fraction
import matplotlib.pyplot as plt

# Oldal beállítása mobilra
st.set_page_config(page_title="Báziscsere App", layout="centered")

st.title("📱 Báziscsere Program")

# Alapadatok beállítása
col1, col2 = st.columns(2)
with col1:
    rows = st.number_input("Sorok (m)", min_value=1, value=3)
with col2:
    cols = st.number_input("Oszlopok (n)", min_value=1, value=3)

# Táblázat inicializálása
if 'matrix' not in st.session_state:
    st.session_state.matrix = np.zeros((rows + 2, cols + 1), dtype=object)
    for i in range(rows + 2):
        for j in range(cols + 1):
            st.session_state.matrix[i, j] = "0"

st.subheader("Táblázat kitöltése")
st.write("Koppints a cellába az érték megadásához (törtet is ér: pl. 1/3):")

# Interaktív táblázat mobilbarát módon
for i in range(rows + 2):
    columns = st.columns(cols + 1)
    for j in range(cols + 1):
        label = f"R{i}C{j}"
        st.session_state.matrix[i, j] = columns[j].text_input("", value=st.session_state.matrix[i, j], key=label, label_visibility="collapsed")

# Báziscsere logika (Pivotálás)
pivot_row = st.number_input("Pivot sor index", min_value=0, max_value=rows-1, value=0)
pivot_col = st.number_input("Pivot oszlop index", min_value=0, max_value=cols-1, value=0)

if st.button("Báziscsere végrehajtása", type="primary"):
    # Itt fut le a báziscsere algoritmusod...
    st.success("Számítás kész!")
    # Grafikon megjelenítése (Matplotlib)
    fig, ax = plt.subplots()
    ax.plot([0, 1], [0, 1], label="Célfüggvény") # Példa
    st.pyplot(fig)
