# job-scheduler
<!DOCTYPE html>
<html>
<head>
  <meta charset='utf-8' />
  <meta name='viewport' content='width=device-width, initial-scale=1.0' />
  <title>Advanced Job Scheduler</title>
  <link href='https://cdn.jsdelivr.net/npm/fullcalendar@6.1.8/index.global.min.css' rel='stylesheet' />
  <style>
    body { font-family: Arial, sans-serif; margin: 0; padding: 0; }
    #calendar { max-width: 900px; margin: 40px auto; padding: 0 10px; }
    .fc-event { cursor: pointer; }
    .color-Walmart { background-color: #f39c12 !important; }
    .color-Grocery { background-color: #27ae60 !important; }
    .color-Other { background-color: #3498db !important; }
  </style>
</head>
<body>
  <h2 style="text-align:center;">Advanced Job Scheduler</h2>
  <div id='calendar'></div>

  <script src='https://cdn.jsdelivr.net/npm/fullcalendar@6.1.8/index.global.min.js'></script>
  <script>
    const jobs = [
      { id: '22666001', title: 'Pest Control - WALMART', start: '2025-05-08', city: 'Powell River', type: 'Walmart' },
      { id: '22666002', title: 'Pest Control - SAFEWAY', start: '2025-05-09', city: 'Powell River', type: 'Grocery' },
      { id: '22666003', title: 'Orkin Aire - Local Office', start: '2025-05-12', city: 'Gibsons', type: 'Other' }
    ];

    function getColorClass(type) {
      switch(type) {
        case 'Walmart': return 'color-Walmart';
        case 'Grocery': return 'color-Grocery';
        default: return 'color-Other';
      }
    }

    document.addEventListener('DOMContentLoaded', function() {
      var calendarEl = document.getElementById('calendar');
      var calendar = new FullCalendar.Calendar(calendarEl, {
        initialView: 'dayGridMonth',
        editable: true,
        selectable: true,
        events: jobs.map(job => ({
          id: job.id,
          title: job.title,
          start: job.start,
          className: getColorClass(job.type),
          extendedProps: {
            city: job.city,
            type: job.type
          }
        })),
        eventClick: function(info) {
          const props = info.event.extendedProps;
          alert(`Job: ${info.event.title}\nCity: ${props.city}\nType: ${props.type}\nScheduled: ${info.event.start.toDateString()}`);
        },
        eventDrop: function(info) {
          const jobId = info.event.id;
          const newDate = info.event.start.toISOString().split('T')[0];
          alert(`Job ${jobId} rescheduled to ${newDate}`);
        }
      });
      calendar.render();
    });
  </script>
</body>
</html>
