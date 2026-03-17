import streamlit as st

st.title("⚖️ Organizador Pré-Audiência")

processo = st.text_input("Número do processo")

st.subheader("Prova Testemunhal")

autor_prova = st.selectbox("Autor pediu prova?", ["Não", "Sim"])
autor_rol = st.selectbox("Autor apresentou rol?", ["Não", "Sim"])

reu_prova = st.selectbox("Réu pediu prova?", ["Não", "Sim"])
reu_rol = st.selectbox("Réu apresentou rol?", ["Não", "Sim"])

intimacao_reu = st.selectbox(
    "Intimação do réu",
    ["Não se aplica", "Pendente", "Cumprido", "AR negativo"]
)

if st.button("Analisar"):

    pendencias = []

    if autor_prova == "Sim" and autor_rol == "Não":
        pendencias.append("Autor não apresentou rol")

    if reu_prova == "Sim" and reu_rol == "Não":
        pendencias.append("Réu não apresentou rol")

    if intimacao_reu == "Pendente":
        pendencias.append("Intimação do réu pendente")

    if intimacao_reu == "AR negativo":
        pendencias.append("Intimação inválida (AR negativo)")

    if len(pendencias) == 0:
        st.success("✅ Processo apto para audiência")
    else:
        st.error("❌ Processo NÃO apto")

        for p in pendencias:
            st.write("-", p)
