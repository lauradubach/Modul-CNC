# 🧩 Kubernetes Secret Management

## 🔍 Was ist das?

**Kubernetes Secret Management** bezeichnet den sicheren Umgang mit sensiblen Daten in Kubernetes-Clustern.
Ein *Secret* ist eine spezielle Ressource, die vertrauliche Informationen enthält, z. B.:

* Passwörter
* API-Schlüssel
* Tokens
* TLS-Zertifikate
* Datenbank-Zugangsdaten

Secrets können Pods über **Umgebungsvariablen** oder **Volumes** bereitgestellt werden.

## ⚙️ Herausforderungen

1. 🔒 **Speicherung im Klartext (Base64)**

   * Secrets sind nur Base64-kodiert, nicht verschlüsselt.
   * Ohne zusätzliche Maßnahmen sind sie lesbar (z. B. in etcd).

2. 🧠 **Zugriffs- und Rollenverwaltung (RBAC)**

   * Unsichere oder zu weit gefasste Berechtigungen sind häufig.
   * Zugriff sollte stark eingeschränkt werden.

3. ♻️ **Lebenszyklus und Rotation**

   * Kubernetes bietet keine automatische Rotation ablaufender Secrets.

4. ☁️ **Integration externer Secret Stores**

   * Externe Systeme wie HashiCorp Vault, AWS Secrets Manager, Azure Key Vault oder Google Secret Manager werden oft verwendet.
   * Dafür sind zusätzliche Operatoren oder Plugins nötig (z. B. *External Secrets Operator*).

5. 🪪 **Audit und Compliance**

   * Nachvollziehbarkeit: Wer hat wann welches Secret erstellt oder geändert?

## ⚖️ Unterschied: Secret vs. ConfigMap

| Merkmal              | **ConfigMap**                 | **Secret**                            |
| -------------------- | ----------------------------- | ------------------------------------- |
| **Zweck**            | Nicht-sensitive Konfiguration | Vertrauliche Daten                    |
| **Speicherung**      | Base64-kodiert, lesbar        | Base64-kodiert, Zugriff eingeschränkt |
| **Sicherheit**       | Keine spezielle Absicherung   | Kann in etcd verschlüsselt werden     |
| **Typischer Inhalt** | `APP_MODE=production`         | `DB_PASSWORD=supersecret`             |

👉 **Merke:**

* **ConfigMap** → normale Konfiguration
* **Secret** → sensible Daten (mit Sicherheitsmaßnahmen)

## 🧠 Best Practices

1. 🔐 **Verschlüsselung at rest aktivieren** (`EncryptionConfiguration` in etcd)
2. ⚖️ **RBAC restriktiv konfigurieren**
3. 🚫 **`kubectl get secrets` nur autorisierten Nutzern erlauben**
4. ☁️ **Externe Secret Stores integrieren** (z. B. Vault, AWS Secrets Manager)
5. ♻️ **Automatische Secret-Rotation implementieren**
6. 🧾 **Secrets nie im Git speichern** (auch nicht Base64)
7. 🕵️ **Audit-Logging aktivieren**