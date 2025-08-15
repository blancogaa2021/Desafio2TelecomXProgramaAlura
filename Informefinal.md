

***

# **Informe Final: Análisis de Evasión de Clientes (Churn) - Telecom X**

## 🔹 **Introducción**
El presente análisis aborda el problema crítico de la evasión de clientes (Churn) en la empresa Telecom X, que actualmente se sitúa en un **25.7%**. El objetivo principal es identificar los factores demográficos, de servicio y contractuales que influyen en la decisión de un cliente de cancelar su contrato. Comprender estos patrones es el primer paso para desarrollar estrategias de retención efectivas, reducir la pérdida de ingresos y mejorar la satisfacción del cliente.

<img width="708" height="553" alt="image" src="https://github.com/user-attachments/assets/c90a91ca-5f48-4a49-a6a9-45de7a36213f" />


---

## 🔹 **Limpieza y Tratamiento de Datos**
Para asegurar la calidad y fiabilidad del análisis, se realizó un robusto proceso de Extracción, Transformación y Carga (ETL). Los pasos clave fueron:

1.  **Desanidación de Datos:** Se utilizó la función `pandas.json_normalize` para aplanar la estructura anidada del archivo JSON original. Las columnas `customer`, `phone`, `internet` y `account` fueron expandidas, transformando una estructura compleja en una tabla analítica funcional de 7.267 filas y 21 columnas.
2.  **Limpieza y Conversión:** Se corrigió el tipo de dato de la columna de cargos totales (`account_Charges_Total`), convirtiéndola de texto a formato numérico y manejando los valores inconsistentes correspondientes a clientes nuevos (con 0 meses de contrato).
3.  **Estandarización y Formateo:** Se renombraron todas las columnas a un formato claro y en español (ej. `account_tenure` a `Meses_Contrato`). Además, se convirtieron variables binarias (como 'Yes'/'No') a un formato numérico (1/0) para posibilitar el análisis cuantitativo y la modelización.

---

## 🔹 **Análisis Exploratorio de Datos (EDA)**
El análisis reveló perfiles de clientes y características de servicio fuertemente asociadas con la tasa de evasión. Las visualizaciones y el análisis de correlación permitieron identificar patrones claros:

* **Perfil del Cliente con Mayor Riesgo de Evasión:** El cliente con mayor probabilidad de cancelar es aquel con un **contrato mes a mes**, que paga con **cheque electrónico** y tiene **pocos meses** en la compañía (la tasa de abandono es más alta en el primer año). Además, estos clientes tienden a pagar **cargos mensuales más altos**, particularmente aquellos con servicio de **Fibra Óptica**.

  <img width="2190" height="690" alt="image" src="https://github.com/user-attachments/assets/a1356da8-748c-423b-9d9d-04822537417c" />


* **Perfil del Cliente Leal:** Por el contrario, el cliente más leal es aquel con **contratos a largo plazo (1 o 2 años)**, una **larga permanencia** en la empresa (más de 24 meses) y que utiliza métodos de pago automáticos como transferencias o tarjeta de crédito.


<img width="1989" height="590" alt="image" src="https://github.com/user-attachments/assets/2f4c02c4-687a-4542-b233-bd7aefff68e4" />


---

## 🔹 **Conclusiones e Insights Clave**

***

## **Análisis de Correlación: Factores de Evasión de Clientes**

La tabla de correlación nos permite cuantificar la relación lineal entre cada característica del cliente y su probabilidad de cancelar el servicio (`Evasion`). Un valor positivo indica que la variable aumenta el riesgo de evasión, mientras que un valor negativo indica que lo reduce, fomentando la lealtad.

---

## **🔴 Factores Clave que Aumentan la Evasión (Correlación Positiva)**
Estas son las señales de alerta más importantes. Los clientes con estas características son los más propensos a cancelar el servicio.

* **Servicio de Internet - Fibra Óptica (+0.30):**
    Aunque es un servicio premium, su alta asociación con el churn sugiere que puede haber problemas relacionados con el **precio**, la **percepción de valor**, o la **estabilidad del servicio** que generan insatisfacción.

* **Método de Pago - Cheque Electrónico (+0.29):**
    Este método no es automático y requiere una acción manual del cliente cada mes. Esto crea un **"punto de decisión" mensual** para reevaluar el gasto, facilitando la cancelación.

* **Cargo Mensual (+0.19):**
    Una relación directa y esperada. A **mayor sea la factura mensual**, mayor es la probabilidad de que un cliente busque alternativas más económicas o decida que el servicio ya no justifica el costo.

* **Facturación Digital (+0.19):**
    Esta correlación sugiere que el perfil de cliente que elige este método (posiblemente más digital y propenso a comparar ofertas en línea) **coincide con el perfil que es más propenso a cambiarse de proveedor**.

* **Ser Adulto Mayor (+0.15):**
    Los clientes mayores de 65 años tienen una ligera tendencia a cancelar más, posiblemente por una mayor **sensibilidad al precio** o a una menor necesidad de servicios complejos.

---

## **🟢 Factores Clave que Reducen la Evasión (Correlación Negativa)**
Estos son los pilares de la retención. Los clientes que presentan estas características son los más leales y valiosos para la empresa.

* **Meses de Contrato (Tenure) (-0.34):**
    Este es el **indicador de lealtad más fuerte**. Cuanto más tiempo un cliente ha estado con la empresa, es mucho menos probable que se vaya. La confianza y la inercia se construyen con el tiempo.

* **Contrato a Dos Años (-0.30):**
    Un compromiso a largo plazo es una barrera de salida muy efectiva. Los clientes con contratos de dos años tienen la tasa de churn más baja, ya que están "atados" al servicio.

* **No Tener Servicio de Internet (-0.22):**
    Un insight muy relevante. Los clientes que **solo tienen servicio telefónico son extremadamente leales**. Probablemente representan un segmento demográfico con necesidades más simples y menos expuesto a la competencia del mercado de internet.

* **Cargo Total (-0.19):**
    Un `Cargo_Total` alto implica que el cliente ha estado pagando durante muchos meses (alta correlación con `Meses_Contrato`). Por lo tanto, es un indicador de la **inversión a largo plazo** y la lealtad del cliente.

* **Contratación de Servicios de Soporte Adicionales:**
    Variables como **`Seguridad_Online_Yes` (-0.17)** y **`Soporte_Tecnico_Yes` (-0.16)** demuestran que los clientes que contratan estos servicios de valor añadido se sienten más protegidos y respaldados, lo que aumenta su dependencia del ecosistema de Telecom X.

---

## **⚪️ Variables de Bajo Impacto**

* **Género (-0.01) y Servicio Telefónico (+0.01):**
    Estas variables tienen una correlación muy cercana a cero, lo que indica que **no son factores relevantes por sí solos** para predecir si un cliente cancelará o no el servicio.

---

## **📊 Conclusión del Análisis de Correlación**

El cliente ideal de Telecom X es aquel que firma un **contrato a largo plazo**, permanece en la compañía por varios años y contrata servicios de soporte adicionales. Por el contrario, el mayor riesgo de evasión proviene de clientes nuevos con **contratos mes a mes**, que pagan facturas mensuales elevadas (especialmente por fibra óptica) y utilizan métodos de pago manuales.

<img width="1402" height="992" alt="image" src="https://github.com/user-attachments/assets/3f53d85e-e61d-43f7-b792-bda9022817eb" />


---

## 🔹 **Recomendaciones Estratégicas**

Basado en los insights anteriores, se proponen las siguientes acciones estratégicas:

1.  **Fomentar Contratos a Largo Plazo:**
    * **Acción:** Crear campañas de marketing y ofertas agresivas para incentivar a los clientes de "mes a mes" a migrar a contratos anuales o de dos años.
    * **Incentivo:** Ofrecer descuentos en la tarifa mensual, un mes de servicio gratis o la inclusión de un servicio adicional (ej. `Seguridad_Online`) sin costo.

2.  **Mejorar el Proceso de Onboarding:**
    * **Acción:** Implementar un programa de seguimiento proactivo para clientes nuevos durante sus primeros 3 meses.
    * **Incentivo:** Realizar llamadas de bienvenida, enviar tutoriales personalizados y ofrecer una revisión gratuita del servicio para asegurar una experiencia inicial óptima.

3.  **Revisar la Estrategia de Precios de Fibra Óptica:**
    * **Acción:** Analizar si el precio del servicio de fibra es competitivo o si la calidad percibida no justifica el costo.
    * **Incentivo:** Considerar la creación de paquetes de servicios (`bundles`) que incluyan `Soporte_Tecnico` o `Proteccion_Dispositivo` a un precio atractivo para aumentar el valor percibido por los clientes de fibra.

4.  **Incentivar Métodos de Pago Automáticos:**
    * **Acción:** Lanzar una campaña para reducir el uso del "cheque electrónico".
    * **Incentivo:** Ofrecer pequeños descuentos recurrentes (ej. $1-$2 al mes) o beneficios a los clientes que registren un método de pago automático (débito automático, tarjeta de crédito), reduciendo la fricción en el proceso de pago.
