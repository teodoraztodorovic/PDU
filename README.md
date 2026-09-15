# PDU
# Semantička segmentacija mamografskih slika na osnovu recepta datog na https://github.com/qubvel-org/segmentation_models.pytorch (UNet++) 

Projekat koristi **U-Net++ sa ResNet34 encoderom** za segmentaciju masa na mamografskim slikama iz **INBreast** dataseta.

## Pokretanje

Notebook je namenjen za pokretanje u **Google Colab-u**.

Potrebno je da se `INBreast.zip` nalazi na Google Drive-u, a zatim po potrebi promeniti putanju:

```python
project_dir = '/content/drive/MyDrive/PDU'
```

Sve potrebne biblioteke se instaliraju na početku notebook-a, tako da je nakon toga dovoljno pokretati ćelije redom.

## Trening

Pre glavnog treninga koristi se **Optuna** za pronalaženje najboljih hiperparametara modela.

Najbolji pronađeni parametri čuvaju se u:

```text
best_params.json
```

Ako ovaj fajl već postoji, Optuna pretraga se neće ponovo pokretati, već će se postojeći parametri učitati i koristiti za trening.

`best_params.json` je postavljen i na **GitHub repozitorijumu**, tako da se može preuzeti i koristiti bez ponovnog pokretanja Optuna pretrage.

Nakon toga se radi **LOPO (Leave-One-Patient-Out) evaluacija**, gde se u svakom prolazu jedan pacijent koristi za testiranje, a ostali za trening.

Rezultati se čuvaju u:

```text
loo_results.csv
```

I ovaj fajl je dostupan na **GitHub repozitorijumu** i može se preuzeti, tako da nije potrebno ponovo pokretati celu LOPO evaluaciju ako su potrebni samo već dobijeni rezultati.

## Finalni model

Na kraju se trenira finalni model sa najboljim pronađenim parametrima.

Model se čuva kao:

```text
final_model.pt
```

Za pokretanje kompletnog treninga dovoljno je pokrenuti notebook ćeliju po ćeliju redom.
