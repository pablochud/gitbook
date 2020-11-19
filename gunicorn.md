```
export PYTHONPATH=/home/<to_project>:/home/<to_project>/apps
gunicorn --preload -c conf.d/gunicorn/conf.py --name ebok-uml-gunicorn --bind 127.0.0.1:8000 toolsv4.wsgi:application
```
