1.1
SELECT*
FROM publications_stats
WHERE theme = 'Мангусты' AND reactions_cnt > 7

1.2
SELECT
  publication_id,
  theme
FROM
  publications_stats

1.3
SELECT
  SUM(reactions_cnt)
FROM
  publications_stats

1.4
SELECT
  SUM(reactions_cnt) reactions_sum
FROM
  publications_stats

1.5
SELECT
  AVG(reactions_cnt) reactions_avg
FROM
  publications_stats
WHERE
  theme = 'Коты' OR theme = 'Собаки'



2.1
SELECT
  *
FROM
  user_comments
WHERE
  DATE_PART('D', time_posted) = 21


2.2
SELECT
  COUNT(*) comments_cnt
FROM
  user_comments
WHERE
  time_posted BETWEEN '2022-08-01' AND '2022-08-15'

2.3
SELECT
  publication_id,
  COUNT(*) comments_cnt
FROM
  user_comments
GROUP BY
  publication_id
ORDER BY
  publication_id

2.4
WITH counter AS(
  SELECT
    publication_id,
    COUNT(*) comments_cnt
  FROM
    user_comments
  GROUP BY
    publication_id
)

SELECT
  AVG(comments_cnt) comments_avg
FROM
  counter


3.1
SELECT
  uco.id,
  uco.user_id
FROM
  user_comments uco
  INNER JOIN users usr ON uco.user_id = usr.id
WHERE
  usr.gender = 'М'
ORDER BY
  uco.id

3.2, 3.3
SELECT
  COUNT(*) users_cnt
FROM
  users usr
  LEFT JOIN user_comments uco ON uco.user_id = usr.id
WHERE
  uco.id is NULL

3.4
SELECT
   avg(length(cmt.text)) as avg_len
FROM
  user_comments uco
  INNER JOIN users usr ON uco.user_id = usr.id
  INNER JOIN comment_text cmt ON uco.id = cmt.comment_id
WHERE
  usr.gender = 'Ж'
  and DATE_PART('month', uco.time_posted) = 7


