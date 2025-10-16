# Writeup Forense: Sequestro do Gato “Gado"

## Cenário

Nosso gato, **Gado**, foi sequestrado. O sequestrador enviou um documento contendo seus pedidos em **MS Word**. Para análise forense, realizamos os seguintes passos:

1. Convertimos o documento Word para **PDF**.
2. Extraímos a **imagem** contida no documento para facilitar a investigação.

**Arquivos obtidos:**

- Documento Word (`.doc`)
- Documento PDF (`.pdf`)
- Imagem extraída (`.jpg`)

---

## Passo 1: Extração de Metadados do PDF

Utilizando ferramentas de análise (ex: `pdfinfo` ou `exiftool`), extraímos os metadados do PDF:

```
Title:           Pay NOW
Subject:         We Have Gato
Author:          Ann Gree Shepherd
```

**Observações:**

- O título e o assunto indicam a urgência e o contexto do sequestro.
- O autor fornece uma possível pista sobre quem criou o documento.

---

## Passo 2: Análise de Metadados da Imagem

Usando `exiftool`, extraímos os metadados da imagem contida no documento:

```
Camera Model Name: Canon EOS R6
```

A imagem também continha informações de **geolocalização (GPS)**:

```
GPS Latitude Ref:  North
GPS Longitude Ref: West
GPS Time Stamp:    13:37:33
GPS Latitude:      51 deg 30' 51.90" N
GPS Longitude:     0 deg 5' 38.73" W
GPS Position:      51 deg 30' 51.90" N, 0 deg 5' 38.73" W
```

---

## Passo 3: Localização

Convertendo as coordenadas GPS no Google Maps, identificamos o local:

**Rua Milk St, Londres, Reino Unido**

---

## Conclusão

A análise forense dos arquivos forneceu informações cruciais:

1. **Autor do documento:** `Ann Gree Shepherd`
2. **Localização do envio ou do sequestro:** `Milk St, Londres, UK`

Esses dados podem ser utilizados para contatar as autoridades locais e auxiliar na recuperação do gato **Gado**.
