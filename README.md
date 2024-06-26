﻿# cadastro-de-pedidos
# cadastro-de-pedidos
# cadastro-de-pedidos
from datetime import datetime
from reportlab.lib.pagesizes import letter
from reportlab.pdfgen import canvas

def obter_dados():
    print("Por favor, preencha as informações abaixo:")
    nome = input("Nome completo: ")
    cpf = input("CPF: ")
    contato = input("Número de contato: ")
    tipo_encomenda = input("Tipo de encomenda: ")
    data_entrega = input("Data e hora da entrega (DD/MM/AAAA HH:MM): ")
    endereco = input("Endereço: ")
    
    # Converter a data de entrega para o formato datetime
    data_entrega = datetime.strptime(data_entrega, "%d/%m/%Y %H:%M")

    return nome, cpf, contato, tipo_encomenda, data_entrega, endereco

def imprimir_demonstrativo(nome, cpf, contato, tipo_encomenda, data_entrega, endereco):
    # Definindo o caminho absoluto para o arquivo PDF
    pdf_file = "demonstrativo_encomenda.pdf"
    
    c = canvas.Canvas(pdf_file, pagesize=letter)
    
    # Definindo as informações a serem impressas no PDF em uma coluna
    c.setFont("Helvetica-Bold", 12)
    c.drawString(50, 750, "Encomenda Realizada com Sucesso:")
    c.drawString(50, 730, "-" * 50)  # Linha separadora

    c.setFont("Helvetica", 12)
    c.drawString(50, 700, "Nome completo:")
    c.drawString(200, 700, nome)
    c.drawString(50, 680, "CPF:")
    c.drawString(200, 680, cpf)
    c.drawString(50, 660, "Número de contato:")
    c.drawString(200, 660, contato)
    c.drawString(50, 640, "Tipo de encomenda:")
    c.drawString(200, 640, tipo_encomenda)
    c.drawString(50, 620, "Data e hora da entrega:")
    c.drawString(200, 620, data_entrega.strftime('%d/%m/%Y %H:%M'))
    c.drawString(50, 600, "Endereço:")
    c.drawString(200, 600, endereco)

    # Salvando o PDF
    c.save()
    print(f"A encomenda foi registrada com sucesso! O demonstrativo foi gerado em '{pdf_file}'.")

def main():
    nome, cpf, contato, tipo_encomenda, data_entrega, endereco = obter_dados()
    imprimir_demonstrativo(nome, cpf, contato, tipo_encomenda, data_entrega, endereco)

if __name__ == "__main__":
    main()
