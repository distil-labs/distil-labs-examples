# Problem setting

Imagine you work for a workplace safety and health organization tasked with developing an automated system to classify workplace injury reports based on free-text narratives. In such a system, improving classification accuracy leads to better incident tracking, more effective prevention strategies, and enhanced workplace safety programs - key objectives in occupational health and safety management.

We will base our example on a [comprehensive workplace incident dataset](https://huggingface.co/datasets/mayerantoine/injury-narrative-coding) that contains injury narratives and their corresponding classification according to the Occupational Injuries and Illnesses Classification System (OIICS). The dataset focuses on seven major categories that encompass the primary types of workplace incidents:

- Violence and other injuries by persons and animals
- Transportation incidents
- Fires and explosions
- Falls, slips, and trips
- Exposure to harmful substances or environments
- Contact with objects and equipment
- Overexertion and bodily reaction

The dataset has two columns containing the OIICS classification code and the injury narrative (including incident description and relevant details). Converting unstructured narrative text into standardized classification codes is crucial for systematic analysis of workplace safety trends, development of targeted prevention strategies, and compliance with safety regulations.