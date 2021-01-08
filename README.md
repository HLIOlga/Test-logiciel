# Quick Chart
_**Projet de Test Logiciel**_

_**Author : Huiling BAO & Heyang LI**_

Introduction général
--
Un logiciel de chat d'entreprise pour développeurs:
- Pourra être exécuté dans un terminal
- Devra avoir un système d’authentification
- Les salles pourront être publiques ou privées
- Il devra y avoir un historique
- Il n’y aura probablement pas plus de 20 personnes par salle
- Côté architecture, les ressources sont limitées mais un serveur pourra être mis à disposition

Architecture de base des données
--
Afin de réaliser ce logiciel, il doit d'abord créer une base des données pour sauvegarder les données utiles et en utilisant ces données pour contrôler le système.

| Room |[id_room] INTEGER|[room_name] text|[room_type] text|
| :------------: | :------------: | :------------: | :------------: |

| User |[id_user] INTEGER|[user_name] text|[user_role] integer|[user_rights] integer|[user_password] text|
| :------------: | :------------: | :------------: | :------------: | :------------: | :------------: |

Donc la processus de contôler ce systèmes peut faciliter par les opérations de SQL.
- Ajouter les valeur : `add_room` et `add_user`
- Sélectionner les valeurs : `get_rooms` et `get_users`
- Supprimer les valeurs : `delete_room` et `delete_user`

Système d'authentification
--
- Nous avons besoin de vérifiez que le mot de passe a un numéro, un caractère spécial, une longueur> 8.

```python
def verify_user_password(user_password):
	# Extra requirement: check the password have number,special character, length>8 
	is_number = 0
	special_character = 0

	for i in user_password:
		if i.isdigit():
			is_number = 1

		if (not i.islower()) and (not i.isupper())  and (not i.isdigit()):
			special_character = 1

	if len(user_password)>=8:
		if is_number and special_character:
			return True

	return False
```

Salles publiques ou privées
--
- Room\_name doit commencer par ROOM\_ et comporter plus de 8 caractères

```python
def verify_room_name(room_name):
	# Extra requirement: room_name start with ROOM_ and length >=8
	if room_name.startswith('ROOM_'):
		if len(room_name) >= 8 :
			return True
	return False
```
- Le type de room doit définir en publiques ou privées

```python
def verify_room_type(room_type):
	# Extra requirement: room_type has to be public or private
	if room_type == 'public' or room_type == 'private':
		return True
	return False
```
