

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

* **El Contrato es el Factor Determinante:** El tipo de contrato **"mes a mes"** es el indicador con la correlación positiva más fuerte (+0.41) con la evasión. La falta de un compromiso a largo plazo facilita la salida del cliente ante cualquier inconveniente o mejor oferta de la competencia.

* **La Experiencia Inicial es Crítica:** La tasa de evasión es masiva en los primeros meses. Esto sugiere problemas en el proceso de **onboarding**, en la configuración de expectativas o en la primera experiencia con la calidad del servicio.

* **El Precio y la Conveniencia son Relevantes:** Clientes con **cargos mensuales elevados** (especialmente entre $70 y $100) y aquellos que utilizan **métodos de pago manuales** (cheque electrónico, correlación de +0.30) son significativamente más propensos a cancelar. La combinación de un servicio premium (Fibra Óptica) con un método de pago de alta fricción parece ser una receta para el churn.

* **Los Servicios de Soporte Generan Retención:** Variables como **`Seguridad_Online`** y **`Soporte_Tecnico`** mostraron una correlación negativa con la evasión. Esto indica que los clientes que contratan estos servicios de valor añadido se sienten más seguros y respaldados, lo que aumenta su lealtad.

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
