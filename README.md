"# l2-exercicio-2" </br>
O projeto é simplesmente um arquivo sqlite3, vi que mencionava o uso de linguagem, mas achei que não precisava, como era simplesmente
uma consulta foi o que fiz</br>

Como rodar:</br>
  Baixe o arquivo e com editor sqlite3 faça a consulta </br>

 ✅  1.Consulta com os horas que os professores têm comprometidas em aulas</br>

 SELECT
    p.name AS professor_name,
    SUM((strftime('%s', cs.end_time) - strftime('%s', cs.start_time)) / 3600.0) AS total_hours
FROM
    PROFESSOR p
        JOIN
    SUBJECT s ON s.professor_id = p.id
        JOIN
    CLASS c ON c.subject_id = s.id
        JOIN
    CLASS_SCHEDULE cs ON cs.class_id = c.id
GROUP BY
    p.name
ORDER BY
    total_hours DESC;


Saída</br>

Professor Girafales     | 6.0</br>
Professora Florinda     | 2.0</br>
Professor Jirafales Jr. | 2.0</br>
Professor Madruga       | 2.0</br>
Professora Clotilde     | 2.0</br>


✅ 2. Lista de salas com horários ocupados</br>

SELECT 
    r.id AS room_id,
    b.name AS building,
    cs.day_of_week,
    cs.start_time,
    cs.end_time
FROM 
    ROOM r
JOIN 
    BUILDING b ON b.id = r.building_id
JOIN 
    CLASS_SCHEDULE cs ON cs.room_id = r.id
ORDER BY 
    r.id, cs.day_of_week, cs.start_time;
    
Saída</br>

Sala 1 | Segunda   | 08:00 | 10:00</br>
Sala 1 | Segunda   | 10:00 | 12:00</br>
Sala 1 | Quarta    | 08:00 | 10:00</br>
Sala 1 | Quarta    | 10:00 | 12:00</br>
Sala 2 | Terça     | 08:00 | 10:00</br>
Sala 2 | Terça     | 14:00 | 16:00</br>
Sala 2 | Quinta    | 08:00 | 10:00</br>


