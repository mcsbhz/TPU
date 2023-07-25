# TPU
Tabela Processual Unificada
import PyPDF2
import re

def find_expressions_in_pdf(pdf_file, expressions):
    # Abre o arquivo PDF
    with open(pdf_file, 'rb') as file:
        reader = PyPDF2.PdfFileReader(file)
        num_pages = reader.numPages

        # Loop através de todas as páginas do PDF
        for page_num in range(num_pages):
            page = reader.getPage(page_num)
            page_text = page.extractText()

            # Procura as expressões no texto da página
            for expression in expressions:
                matches = re.findall(expression, page_text, re.IGNORECASE)
                if matches:
                    print(f'Página {page_num + 1}: Encontrado "{expression}"')
                    print('Correspondências:', matches)

if __name__ == "__main__":
    pdf_file = 'example.pdf'
    expressions_to_find = ['exemplo', 'Python']
    find_expressions_in_pdf(pdf_file, expressions_to_find)
