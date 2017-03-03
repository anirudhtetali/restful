       query = connect.execute("select Date from daily")
        data = {'Date': [dict(zip(tuple (query.keys()) ,i)) for i in query.cursor]}
        if data == {"Date": []}:
            return "Data not found"
        else:
            return data
from flask import Flask, request, make_response, jsonify, abort
from flask_restful import Resource, Api
from sqlalchemy import create_engine

dbs = create_engine('sqlite:///cincydb.db')

app = Flask(__name__)
api = Api(app)

class historicalone(Resource):
    def get(self):
        connect = dbs.connect()
        query = connect.execute("select Date from daily")
        data = {'Date': [dict(zip(tuple (query.keys()) ,i)) for i in query.cursor]}
        if data == {"Date": []}:
            return "Data not found"
        else:
            return data


class historicaltwo(Resource):
    def get(self, date):
        connect = dbs.connect()
        query = connect.execute("select * from daily where Date='%s'"%date)
        data = {'Date': [dict(zip(tuple (query.keys()) ,i)) for i in query.cursor]}
        if data == {"Date": []}:
            return "Data not found"
        else:
            return data

@app.route('/historical/delete/<string:date>', methods=['GET','DELETE'])
def delete(date):
        connect = dbs.connect()
        query = connect.execute("delete from daily where Date='%s'"%date)
        return make_response(jsonify({'Date deleted for': date}), 200)

class putvalue(Resource):
    def get(self, date, Tmax, Tmin):
        connect = dbs.connect()
        query = connect.execute("insert into daily(Date, Tmax, Tmin) values (?, ?, ?)",(date,Tmax,Tmin))
        return make_response(jsonify({'Date': date, 'Tmax': Tmax, 'Tmin': Tmin}), 201)

class prediction(Resource):
  def get(self, date):
    connect = dbs.connect()
    dayone = int(date)
    end_date = dateone + 7
    query = connect.execute("SELECT @Date := @Date + 1 Date, RANDOM()*(TMAX*2),RANDOM()*(TMIN*2) FROM daily, (SELECT @Date := ?) rows ORDER BY Date limit 7", (dateone))
    data = {'Date': [dict(zip(tuple (query.keys()) ,i)) for i in query.cursor]}
    if data == {"Date": []}:
        return "Data not found"
    else:
        return data

api.add_resource(historicalone, '/historical/')
api.add_resource(historicaltwo, '/historical/<string:date>')
api.add_resource(putvalue, '/historical/<string:date>,<string:Tmax>,<string:Tmin>')
api.add_resource(prediction, '/historical/forecast/<string:date>')
if __name__ == '__main__':
     app.run(debug=True)

