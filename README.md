# Movie-Data
Movie data analysis

## 1. managers and the stores 

SELECT concat(st.first_name," ",st.last_name) as Fullname, ad.address, ad.district, cy.city, co.country
FROM sql_project.staff st
INNER JOIN address ad
	ON st.address_id = ad.address_id
INNER JOIN city cy
	ON ad.city_id = cy.city_id
INNER JOIN country co
	ON cy.country_id = co.country_id
GROUP BY ad.address, ad.district, cy.city, co.country
ORDER BY Fullname;


#### 2. Inventory Request

SELECT iv.inventory_id, 
	iv.film_id, 
	iv.store_id, 
    title, 
    f.replacement_cost,  
    f.rating
FROM sql_project.inventory iv
INNER JOIN film f
	ON iv.film_id = f.film_id
GROUP BY title
ORDER BY f.replacement_cost DESC;



### 3. Summary overview for each rating at each store


SELECT iv.inventory_id, iv.store_id, f.title, f.rating
FROM sql_project.inventory iv
INNER JOIN film f
	ON iv.film_id = f.film_id
GROUP BY title
ORDER BY f.title;


### 4. Inventory Diversity

SELECT iv.inventory_id, 
	iv.film_id, 
	iv.store_id, 
	ct.name, 
	f.title, 
    f.rating,
	AVG(f.replacement_cost) AverageReplacementCost, 
	SUM(f.replacement_cost) TotalReplacementCost,
	SUM(DISTINCT iv.film_id) numberOfFilms
FROM sql_project.inventory iv
INNER JOIN film f
	ON iv.film_id = f.film_id
INNER JOIN category ct
	ON f.film_id = ct.category_id
GROUP BY   title;

#### 5. CUSTOMER INFORMATION

SELECT CONCAT(cu.first_name," ",cu.last_name) Fullname, 
	ad.address, 
	cu.active,
    cy.city,
	co.country
	FROM sql_project.customer cu
JOIN address ad
	ON cu.address_id = ad.address_id
JOIN city cy
	ON ad.city_id = cy.city_id
JOIN country co
	ON cy.country_id = co.country_id;
    
    
    
### 6. Most Valuable Customers

SELECT cu.first_name, cu.last_name,
	SUM(DISTINCT p.amount) TotalAmount,
    COUNT(r.customer_id) TotallifetimeRentals
    FROM customer cu
JOIN payment p
	ON cu.customer_id = p.customer_id
JOIN rental r
	ON p.rental_id = r.rental_id
GROUP BY 1,2
ORDER BY TotalAmount DESC;



### 7. Advisors and current investors


SELECT CONCAT(iv.first_name," ",iv.last_name) Invenstor_Fullname, 
	iv.company_name,
	CONCAT(ad.first_name," ",ad.last_name) Advisor_Fullname, ad.is_chairmain
FROM investor iv
JOIN advisor ad
	ON iv.investor_id = ad.advisor_id;
    
    
### 8. Most Awarded actors

    
    SELECT aw.first_name, 
		aw.last_name,
        awards,
        COUNT(*) aw_count
	FROM actor_award aw
	JOIN film f	
		ON aw.actor_id = f.film_id
	GROUP BY first_name;
	
        
    




















