import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt

def generate_data():
    data = {
        'Linguagem': ['Python', 'Dart', 'C++', 'C', 'Java'],
        'Dominio': [35, 30, 20, 10, 5],
        'Color': ['#e5d720', '#370c5f', '#20afe5', '#203ee5', '#e8401c']
    }
    return pd.DataFrame(data)

def display_horizontal_line(data):
    fig, ax = plt.subplots(figsize=(100, 1))
    fig.patch.set_facecolor('none')
    ax.set_yticks([])
    ax.set_xlim(0, 100)
    ax.set_ylim(0, 0)
    for index, row in data.iterrows():
        ax.barh(0, row['Dominio'], color=row['Color'], left=data['Dominio'][:index].sum(), linewidth=0)
    ax.grid(False)
    ax.xaxis.set_tick_params(labelbottom=False)
    for spine in ax.spines.values():
        spine.set_visible(False)

    st.pyplot(fig)

def display_legend(data):
    fig, ax = plt.subplots(figsize=(5, 2))
    fig.patch.set_facecolor('none')

    n_items = len(data)
    n_cols = 2
    n_rows = -(-n_items // n_cols)

    for index, row in data.iterrows():
        col = index % n_cols
        row_ = index // n_cols
        x = col * 4 + 1.2 
        y = 1 - row_ * 0.8
        ax.scatter(x, y, color=row['Color'], s=90, marker='o')
        ax.text(x + 0.2, y, f"{row['Linguagem']} ({row['Dominio']})", verticalalignment='center', fontsize=7, color='yellow', fontstyle='italic')

    ax.axis('off')

    st.pyplot(fig)

def main():
    st.markdown("<h1 style='color: white; margin-bottom: 0;'>printf(''Hello World, i'm Levy'')</h1>", unsafe_allow_html=True)
    st.markdown("<hr style='border: 1px solid #3a3a3a; margin: 1px 0;'>", unsafe_allow_html=True)
    st.markdown("<h1 style='color: #5162c3; margin-top: 10;'>My degree of familiarity with each language</h1>", unsafe_allow_html=True)

    data = generate_data()

    display_horizontal_line(data)
    display_legend(data)

if __name__ == "__main__":
    main()
