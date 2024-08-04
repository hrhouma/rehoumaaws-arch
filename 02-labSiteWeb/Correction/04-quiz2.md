# Script MySQL:

- Ce quiz a pour objectif de vérifier votre compréhension et de votre capacité à utiliser diverses commandes MySQL pour gérer la base de données `cafe_db`.
- Considérez le script suivant : 

```sql
show databases;
use cafe_db;
show tables;
select * from product;
exit;

create table orders (order_id int, product_id int, quantity int, order_date datetime);
insert into orders (order_id, product_id, quantity, order_date) values (1, 1, 2, now());
select * from orders;
update orders set quantity = 3 where order_id = 1;
delete from orders where order_id = 1;

create index idx_product_id on product(product_id);
drop index idx_product_id on product;

alter table product add column description text;
alter table product drop column description;

truncate table orders;
rename table orders to customer_orders;

grant all privileges on cafe_db.* to 'user'@'localhost';
revoke all privileges on cafe_db.* from 'user'@'localhost';

backup database cafe_db to disk = '/var/backups/cafe_db.bak';
restore database cafe_db from disk = '/var/backups/cafe_db.bak';
```


# Instructions :

Répondez aux questions suivantes en cochant la bonne réponse. Certaines questions peuvent avoir plus d'une réponse correcte.

---

**Question 1:** Quelle commande est utilisée pour sélectionner la base de données `cafe_db` ?

A. `show databases;`  
B. `use cafe_db;`  
C. `show tables;`  
D. `select * from product;`  

---

**Question 2:** Quelle commande est utilisée pour afficher toutes les tables dans la base de données sélectionnée ?

A. `show databases;`  
B. `use cafe_db;`  
C. `show tables;`  
D. `select * from product;`  

---

**Question 3:** Quelle commande est utilisée pour insérer une nouvelle ligne dans la table `orders` ?

A. `create table orders (order_id int, product_id int, quantity int, order_date datetime);`  
B. `insert into orders (order_id, product_id, quantity, order_date) values (1, 1, 2, now());`  
C. `select * from orders;`  
D. `update orders set quantity = 3 where order_id = 1;`  

---

**Question 4:** Quelle commande est utilisée pour mettre à jour une ligne existante dans la table `orders` ?

A. `create table orders (order_id int, product_id int, quantity int, order_date datetime);`  
B. `insert into orders (order_id, product_id, quantity, order_date) values (1, 1, 2, now());`  
C. `select * from orders;`  
D. `update orders set quantity = 3 where order_id = 1;`  

---

**Question 5:** Quelle commande est utilisée pour supprimer une ligne de la table `orders` ?

A. `create table orders (order_id int, product_id int, quantity int, order_date datetime);`  
B. `delete from orders where order_id = 1;`  
C. `select * from orders;`  
D. `update orders set quantity = 3 where order_id = 1;`  

---

**Question 6:** Quelle commande est utilisée pour créer un index sur la colonne `product_id` de la table `product` ?

A. `create index idx_product_id on product(product_id);`  
B. `drop index idx_product_id on product;`  
C. `alter table product add column description text;`  
D. `alter table product drop column description;`  

---

**Question 7:** Quelle commande est utilisée pour ajouter une colonne `description` à la table `product` ?

A. `create index idx_product_id on product(product_id);`  
B. `drop index idx_product_id on product;`  
C. `alter table product add column description text;`  
D. `alter table product drop column description;`  

---

**Question 8:** Quelle commande est utilisée pour vider la table `orders` ?

A. `truncate table orders;`  
B. `delete from orders where order_id = 1;`  
C. `update orders set quantity = 3 where order_id = 1;`  
D. `select * from orders;`  

---

**Question 9:** Quelle commande est utilisée pour renommer la table `orders` en `customer_orders` ?

A. `truncate table orders;`  
B. `rename table orders to customer_orders;`  
C. `drop index idx_product_id on product;`  
D. `grant all privileges on cafe_db.* to 'user'@'localhost';`  

---

**Question 10:** Quelle commande est utilisée pour sauvegarder la base de données `cafe_db` ?

A. `grant all privileges on cafe_db.* to 'user'@'localhost';`  
B. `revoke all privileges on cafe_db.* from 'user'@'localhost';`  
C. `backup database cafe_db to disk = '/var/backups/cafe_db.bak';`  
D. `restore database cafe_db from disk = '/var/backups/cafe_db.bak';`  

