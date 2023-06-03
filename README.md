# Reto 12

Hacer un programa que lea archivos y presentar.

- Cantidad de vocales
- Cantidad de consonantes
- Listado de las 50 palabras que más se repiten
- Listado de destinatarios con cantidad de mensajes recibidos
- Cantidad de mensajes enviados por cada día

Tener en cuenta que el archivo que se quiere procesar tiene que estar dentro de la misma carpeta en la que esta alojada el programa y que tenga explicitamente el nombre "archivo.txt" 

```Python
import re
from collections import Counter
with open('archivo.txt', 'r') as file:  # Leer el archivo de texto
    text = file.read().lower()
vowels = re.findall('[aeiou]', text)    # Contar el numero de vocales y consonantes
consonants = re.findall('[bcdfghjklmnpqrstvwxyz]', text)
print('numero de vocales:', len(vowels))
print('numero de consonantes:', len(consonants))
words = re.findall(r'\w+', text)    # Obtener las 50 palabras mas repetidas
word_count = Counter(words)
top_words = word_count.most_common(50)
print('50 palabras mas repetidas:', top_words)
with open('emails.txt', 'r') as file:      # Contar la cantidad de mensajes recibidos y enviados cada dia
    emails = file.read()
recipients = re.findall('To: (.+)', emails) # Obtener la lista de destinatarios y remitentes
senders = re.findall('From: (.+)', emails)
received_count = Counter()  # Contar la cantidad de mensajes recibidos y enviados por dia
sent_count = Counter()
dates = re.findall('Date: .+', emails)
for date in dates:
    day = date.split(', ')[1].split(' ')[0]
    if any(recipient in date for recipient in recipients):
        received_count[day] += 1
    if any(sender in date for sender in senders):
        sent_count[day] += 1
print('Cantidad de mensajes recibidos por dia:', received_count)
print('Cantidad de mensajes enviados por dia:', sent_count)
```
