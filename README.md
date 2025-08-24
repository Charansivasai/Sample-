SELECT 
    c.customer_id,
    c.customer_name,
    ph.current_policy_type,
    ph.current_policy_amt,
    ph.previous_policy_type,
    ph.previous_policy_amt
FROM policy_history ph
JOIN customers c 
    ON c.customer_id = ph.customer_id
WHERE ph.current_policy_type <> ph.previous_policy_type;


SELECT 
    c.customer_id,
    c.customer_name,
    'All' AS region,
    SUM(p.policy_amt) AS total_policy_amt
FROM customers c
JOIN policies p 
    ON c.customer_id = p.customer_id
GROUP BY c.customer_id, c.customer_name;

SELECT 
    c.customer_id,
    c.customer_name,
    'All' AS region,
    p.policy_type,
    SUM(p.policy_amt) AS total_policy_amt
FROM customers c
JOIN policies p 
    ON c.customer_id = p.customer_id
WHERE p.policy_type = 'Auto'
GROUP BY c.customer_id, c.customer_name, p.policy_type;

SELECT 
    c.customer_id,
    c.customer_name,
    'East and West' AS region,
    p.policy_term,
    p.policy_start_dt,
    SUM(p.policy_amt) AS total_policy_amt
FROM customers c
JOIN policies p 
    ON c.customer_id = p.customer_id
WHERE c.region IN ('East', 'West')
  AND p.policy_term = 'Quarterly'
  AND YEAR(p.policy_start_dt) = 2012
GROUP BY c.customer_id, c.customer_name, p.policy_term, p.policy_start_dt;



SELECT 
    c.customer_id,
    c.customer_first_name,
    c.customer_last_name,
    c.customer_segment,
    mh.marital_status,
    mh.start_dt_marital_status,
    mh.end_dt_marital_status
FROM marital_history mh
JOIN customers c 
    ON c.customer_id = mh.customer_id
WHERE EXISTS (
    SELECT 1
    FROM marital_history mh2
    WHERE mh2.customer_id = mh.customer_id
    AND mh2.marital_status <> mh.marital_status
);

SELECT 
    c.customer_id,
    c.customer_name,
    c.region,
    c.address,
    p.policy_id,
    p.policy_type,
    p.policy_amt,
    p.policy_term,
    p.policy_start_dt
FROM customers c
JOIN policies p 
    ON c.customer_id = p.customer_id;
    

